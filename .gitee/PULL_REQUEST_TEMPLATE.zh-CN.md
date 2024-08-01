<!-- 感谢您提交PR！请按照模板填写，以便审阅者可以轻松理解和评估代码变更的影响。Thanks for submitting a pull request! We appreciate you spending the time to work on these changes. Please follow the template so that the reviewers can easily understand what the code changes affect -->

# Summary

请解释此次更改的 **动机**，以下是一些帮助您的要点：

- 这个 PR 解决了哪些 issues？请标记这些 issues，以便合并 PR 后这些 issues 将会被自动关闭。
- 这个功能是什么？（如果适用）
- 您是如何实现解决方案的？
- 这个更改影响了库的哪些部分？

## Checklist

<!-- 检查项, 请自行排查并打钩, 通过: [X] -->

- [ ] 是否按[最新模板](../zh-cn/model.md)修改；
- [ ] 是否修改模板号，当前最新版本为 v0.2.2；
- [ ] 是否填写 github 地址，位于模板版本下面:[!tip] Github 地址，地址使用 HarmonyOS 仓库地址，若不需要 HarmonyOS 化则填原库地址；
- [ ] 无修改的库是否指定版本，直接可复用社区代码，不涉及各类平台判断（platfrom、文件平台后缀等）的库，npm install & yarn add 需要指定验证的版本；
- [ ] 是否列全所有暴露属性和接口（含不支持的）；
- [ ] Link 路径是否配套；
- [ ] ArkTS 引入是否配套版本；
- [ ] 是否添加权限限制（如有）；
- [ ] 属性章节是否添加平台说明；
- [ ] 属性章节是否使用英文头；
- [ ] 属性章节 Description 是否补充平台描述；
- [ ] 兼容性章节是否区别了“发 release”和“未发 release”；
- [ ] 遗留问题是否有 issue 跟踪；
- [ ] 开源协议是否和原库原库一致（LICENSE）；
- [ ] 有引入原生端代码和依赖是否和 npm 的包名一致；
- [ ] API、静态方法、属性的表格是否按照模板的格式；
- [ ] 不支持属性是否有做问题遗留；
- [ ] 文档是否使用了 prettier 格式化；
- [ ] release 超链接的载体是否为完整库名 + Release;
- [ ] 兼容性模块 RNOH 的版本 0.72.20 以后的版本不需要加 CAPI；
- [ ] 使用 codegen 和直接链接源码的文档链接是否是相对路径；
- [ ] 文档里面的 demo 是否没有代码代码错误，直接可跑通；
- [ ] 文档名字是否以 npm 包名为准；
- [ ] fabric 库是否有 “在 ArkTS 侧引入 xxx 组件”；
