# treedemo

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

## 功能支持
- （隐藏/显示）连接线
- （隐藏/显示）自定义文件夹图标
- 字体
- 链接
- 点击触发事件

### 属性
```ts
enum Status {
  CLOSE,
  OPEN,
}
interface treeType {
  id: string;
  name: string;
  icon?: string;
  status: Status;
  fontCss?: unknown;
  toUrl: () => void | null;
  children?: Array<treeType> | null;
}
interface optionType {
  Tree: Array<treeType>;
  options: {
    showIcon: boolean;
    showLine: boolean;
  };
  firstNodeId?: string; // 解决第一层头个结点css问题
}
```

### 默认
![image](https://raw.githubusercontent.com/JJking666/ATree/master/src/assets/show/1.png)

### 展开
![image](https://raw.githubusercontent.com/JJking666/ATree/master/src/assets/show/2.png)

### 隐藏连接线
![image](https://raw.githubusercontent.com/JJking666/ATree/master/src/assets/show/3.png)

### 隐藏图标
![image](https://raw.githubusercontent.com/JJking666/ATree/master/src/assets/show/4.png)