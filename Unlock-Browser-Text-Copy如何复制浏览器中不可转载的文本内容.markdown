### 教程：如何复制浏览器中不可转载的文本内容

##### 本教程包含谷歌浏览器和Safari浏览器如何复制浏览器中不可转载的文本内容，Safari浏览器在教程开始之前先移到文末打开开发者调试模式

#### 第一步：在谷歌浏览器中按F12打开控制台![截屏2025-09-22 15.31.54](/Users/shenyz/Library/Application Support/typora-user-images/截屏2025-09-22 15.31.54.png)

#### 第二步：点击菜单栏中的Console![截屏2025-09-22 15.32.44](/Users/shenyz/Library/Application Support/typora-user-images/截屏2025-09-22 15.32.44.png)

#### 第三步：输入以下代码到小箭头>后面

```
const nodes = Array.from(document.querySelectorAll('[class*="RichContent"]'));
const summary = nodes.map((e,i)=>({
  idx: i,
  tag: e.tagName,
  className: e.className,
  textLen: (e.innerText || '').length
}));
summary.sort((a,b)=>b.textLen - a.textLen);
console.table(summary.slice(0, 20)); // 显示前20个候选
// 为方便后续操作，把节点数组暴露到全局
window.__RC_NODES = nodes;
```

![截屏2025-09-22 15.34.06](/Users/shenyz/Library/Application Support/typora-user-images/截屏2025-09-22 15.34.06.png)

#### 第四步：得到如图所示表格，将表格中排名最高的一列的idx输入如下代码中相应的位置

例如本图示中排名最高的idx为0，输入到以下代码第二行和第四行中：

```
// 在 Console 中查看该节点对象（可在 Elements 面板展开）
console.log(window.__RC_NODES[0]);
// 快速查看它的部分文本长度与开头（避免一次性打印全部大文本）
const el = window.__RC_NODES[0];
console.log('class:', el.className, 'text length:', (el.innerText||'').length);
console.log((el.innerText||'').slice(0,400)); // 先看前400字符
```

![截屏2025-09-22 15.38.11](/Users/shenyz/Library/Application Support/typora-user-images/截屏2025-09-22 15.38.11.png)

#### 第五步：检查文本是否为所需文本，如是，则再再控制台中输入以下代码

```
const el = window.__RC_NODES[0];
console.log('class:', el.className, 'text length:', (el.innerText||'').length);
console.log((el.innerText||'')); // 打印全部文本
```

![截屏2025-09-22 15.39.57](/Users/shenyz/Library/Application Support/typora-user-images/截屏2025-09-22 15.39.57.png)

#### 第六步：得到结果之后直接复制即可

###  附加步骤：**开启 Safari 开发者调试模式的步骤**

#### **一：启用“开发”菜单**

Safari 的开发者工具隐藏在“开发”菜单下，首先需要开启它。

1. 打开 Safari 浏览器。
2. 点击菜单栏中的 **Safari > 设置**（或按快捷键 `Command + ,`）。
3. 在设置窗口中，切换到 **高级** 标签。
4. 勾选 **“在菜单栏中显示‘开发’菜单”**。

#### **二：打开开发者工具**

完成“开发”菜单的启用后，您会在菜单栏看到一个名为 **“开发”** 的新选项。以下是如何打开开发者工具的方法：

1. **通过右键直接打开**： 

- 右键点击网页上的任意元素，选择 **检查元素**。

1. **通过菜单打开**： 

- 在菜单栏点击 **开发 > 显示 Web 检查器**。

##### Safari 的开发者工具功能与 Chrome DevTools 类似，步骤从上文中第二步开始即可