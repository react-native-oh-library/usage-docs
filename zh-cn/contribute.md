# 贡献文档

非常欢迎您贡献文档，我们鼓励开发者以各种方式参与文档反馈和贡献。您可以对现有文档进行评价、简单更改、反馈文档质量问题、贡献您的原创内容。

## 贡献方式

高质量的问题反馈有助于我们不断完善文档内容和质量，您提供的信息越详尽，对我们问题改进越有帮助。

1. 在Gitee页面中，“Issue”页签中单击“新建Issue”，在标题栏中描述问题，在编辑框中添加详细问题描述。
2. 单击“创建”按钮，提交Issue，耐心等待文档团队成员确认您的问题。

### 简单更改

针对现有文档进行快速更改和修复，适合少量内容修改和补充。

1. 在文档页面右上角单击“编辑“按钮即可跳转到对应的Gitee工程源文件页面。
2. 在Gitee源文件md页面中，在对应内容处完成更改、修复。
3. 修改完成后，可单击“预览“按钮，确认修改结果。

### 贡献HarmonyOS化RN三方库使用文档

新增使用文档：

1. 参考[文档](https://react-native-oh-library.gitee.io/docs/#/zh-cn/third-party?id=%e4%b8%89%e6%96%b9%e5%ba%93%e5%88%86%e7%b1%bb)将三方库按纯JS库/JS库/原生库进行分类，并且根据[模板](./model.md)撰写不同类型的使用文档。

2. 使用[prettier](https://github.com/prettier/prettier)格式化文档，`prettier --write ./xx.md` 。

3. 在根目录[README.md](../README.md)和[zh-cn/README.md](./README.md)补充该库信息，两者内容一致。

4. 在[\_sidebar.md](../_sidebar.md)添加使用文档导航栏配置。

5. 运行`docsify serve` 查看[docsify](https://docsify.js.org/#/quickstart)效果。

6. 新建相关issue，按[校验规则](https://gitee.com/react-native-oh-library/usage-docs/push_config)commit并提交PR到本仓，等待审核人员合入。

   ```
   // commit模板
   [Issues: #I8K7DK] 新增react-native-svg文档
   ```
