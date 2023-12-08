---
title: "MobX 另人失望"
date: 2023-12-08T21:12:32+08:00
draft: false
---

看到 [推上](https://twitter.com/hd_nvim/status/1727038570198979070) 有个老外讲述他如何用 MobX 来解耦业务逻辑和 UI 逻辑时，我被这个理念吸引住了，也决定引入 MobX 一试。业务逻辑被隔离出来后，代码逻辑变清晰了；MobX 也让我可以把 React 的 immutable 理念抛诸脑后，写代码起来也轻松了很多。

但我深度使用时，发现 MobX 时常有反直觉的不刷新问题。

比如有这么一个 `CheckboxList` 组件，它的功能是展示多个复选框，允许用户选中多个：

![a not reactive checkbox list](/image/2023/12/checkbox-list.png)

用这份代码实现：

```tsx
import { Checkbox, Flex } from '@mantine/core';
import { observer } from 'mobx-react-lite';
import React from 'react';

type Props = {
  data: string[];

  selectedItems: string[];
  setSelectedItems: (items: string[]) => void;
};

const CheckboxList = observer(({ data, selectedItems, setSelectedItems }: Props) => {
  return (
    <Flex gap="sm">
      {data.map((item) => (
        <Checkbox
          key={item}
          label={item}
          checked={selectedItems.includes(item)}
          onChange={(event) => {
            let newSelectedItems: string[];
            if (event.currentTarget.checked) {
              newSelectedItems = [...selectedItems, item];
            } else {
              newSelectedItems = selectedItems.filter((selectedItem) => selectedItem !== item);
            }
            newSelectedItems.sort();

            setSelectedItems(newSelectedItems);
          }}
        />
      ))}
    </Flex>
  );
});
CheckboxList.displayName = 'CheckboxList';

export default CheckboxList;
```

它是一份完全合理的 React 代码。但是当你配合使用 MobX 的 observable 时，就会产生问题。下面的使用示例展示这个问题：

```tsx
import { makeAutoObservable } from 'mobx';
import React from 'react';

import CheckboxList from '$src/component/general/CheckboxList';

class C {
  selectedData: string[] = [];

  constructor() {
    makeAutoObservable(this);
  }

  setSelectedData(data: string[]) {
    this.selectedData = data;
  }
}

const data = ['a', 'b', 'c'];

export default function Test() {
  const [c] = React.useState(new C());

  return (
    <CheckboxList 
      data={data}
      selectedItems={c.selectedData}
      setSelectedItems={c.setSelectedData.bind(c)}
    />
  );
}
```

初看这份代码并没有什么问题。但事实上，无论你怎么点击那些复选框，页面都没有一丝变化。

原因在于：MobX 只能在你访问一个 observable（`c`）的属性（`selectedData`）时，才能 reactive 起来。而这份代码里面，我们将 `c.selectedData` 直接传给了 `CheckboxList` 组件，导致界面不 reactive。即是说，点击复选框时，`c.setSelectedData` 的确被调用了，`c.selectedData` 的确被更新了，但是 `CheckboxList` 感知不到这个更新，因此没有体现在 DOM 上。

这真是个很挫的限制。一个 workaround 是，把 `CheckboxList` 接受的 `selectedData` 的类型改了：

```tsx
# 原来
selectedItems: string[];

# 改成
selectedItems: () => string[];
```

调用处改成这样：

```tsx
<CheckboxList 
  data={data}
  selectedItems={() => c.selectedData}
  setSelectedItems={c.setSelectedData.bind(c)}
/>
```

这样每次 `CheckboxList` re-render 时，都会调用到 `c.selectedData`，因此界面又 reactive 起来了。但这实在是很挫的做法。

而且在实际使用 MobX 过程中，发现网络上相关的内容还是挺少的。我选择 MobX 的原因在于：

1. 网络上对 Redux 过于啰嗦的抱怨很多
2. MobX 是发展了很多年的项目，应该相对成熟

但事实上 MobX 并不如我想象中省心。下回会直接用行业标准 RTK。
