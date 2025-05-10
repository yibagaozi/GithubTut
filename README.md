# GithubTut
示例仓库链接：[https://github.com/yibagaozi/GithubTut](https://github.com/yibagaozi/GithubTut)

### GitHub 主要功能
- **克隆（Clone）**：将远程仓库复制到本地，创建一份本地副本，在自己电脑上查看和编辑代码，建立分支并开发功能​。
- **提交（Commit）**：将新增或修改的代码保存为一个新的版本，提交到仓库指定分支中。每次commit会记录修改内容和说明，形成项目的历史记录。GitHub上可以看到每次提交的记录和差异比较，便于追踪变化。commit通常提交至对应的feature分支上，调试过程中修复发现的问题允许提交至dev分支，原则上主分支不允许直接的commit，而是通过合并分支的方式更新。
  - 建议的commit格式：`<type>(<scope>): <short summary> [by <developerName>]`
  - 如：`feat(user): add user authentication [by chaijiayang]`
  - 或者是：`fix: fix user authentication [by chaijiayang]`
- **分支（Branch）管理**：分支是代码开发的平行空间，用于不同成员实现不同的功能而互不干扰。通常从开发分支`dev`创建新分支（如`feature/login`）来开发新特性。开发完成并调试通过后，再将分支合并回开发分支。这样主分支始终保持稳定，而feature分支用于并行开发工作。
  - **我们统一分支命名规则为`feature/<developerName>/<brief-feature-description>`**
  - 如：`feature/chaijiayang/refactor-user-auth`
- **合并（Merge）**：将一个分支的修改整合进另一个分支。在完成功能后，会将功能分支合并到主分支，以整合代码。在合并过程中Git会自动整合不同改动，若同一文件同一位置有冲突需人工解决。合并后，主分支包含了新功能的代码变化。
- **Pull Request（PR，拉取请求）**：GitHub提供的协作机制。开发者在GitHub上提交一个PR，请求将自己分支的更改合并到目标分支（通常是主分支）。团队成员可以在PR中审查代码、更改讨论并提出修改意见。PR通常包含描述、相关Issue链接、代码差异变化等信息。在代码审查通过后，维护者会接受PR并合并代码。
  - **我们统一PR命名规则为`[Feature][<developerName>] <Detailed Feature Description> (#IssueNumber)`**
  - 如：`[Feature][chaijiayang] Refactor user authentication (#1)`，其中IssueNumber为可选项，当PR关联至某个Issue时引用
  - **记得指定Reviewer**
  - 请在comments中简短描述代码修改的内容
- **Issue**：GitHub中Issue用来指出代码中的bug或者进行功能的讨论交流。每个Issue都有编号、标题、描述，团队可以在下面评论沟通。Issue通常与PR相互关联：例如通过在PR描述中引用Issue编号，合并PR时相应Issue可以自动关闭，表示问题解决，或者讲Issue指定给某人解决。
  
以上功能相互配合，实现完整的版本管理流程：开发者从远程克隆仓库，创建新分支进行开发，提交一系列改动并推送到远程，然后打开Pull Request请求合并，由团队进行代码审查，通过后合并到主分支，并使用Issue跟踪和记录整个过程。

### Github 版本管理

![pic1](/git_flow.png)
*流程图：GitHub Flow 分支管理流程示意图。黄色圆点表示功能开发的提交，绿色圆点表示各feature分支向dev分支发起的Pull Request，蓝色圆点表示dev分支向主分支发起的Pull Request，红色圆点表示紧急修复的提交。*

*开发者从dev分支创建新feature分支（功能分支），在feature分支上进行一系列提交开发新功能，准备就绪后通过 Pull Request 将功能分支合并回dev分支发布。*

上述流程图展示了一个常见的GitHub分支开发工作流。
- 首先，主分支（通常为`main`或`master`，蓝色节点）始终保持可用于发布的稳定状态。
- 开发分支（通常为`dev`或`develop`，绿色节点）用于合并各feature分支，以及fix补丁的合入。
- 当需要开发新功能或修复Bug时，从`dev`分支拉出一个功能分支（`feature branch`，黄色）。在功能分支上，我们进行一系列提交（黄色节点依次排列），实现所需的代码改动。开发过程中一般情况下无需与主分支保持同步，只有必要时将主分支最新更改合并或重基到功能分支上，以减少后续冲突。
- 在功能完成并自测代码通过后，发起一个Pull Request，请求将功能分支合并回`dev`分支,并在发起Pull Request时指定Reviewer，对PR进行Code Review和CI自动测试。
- 如果需要修改，相关问题会通过Issue反馈，开发者在同一功能分支继续提交补充，这些新提交会自动更新PR。代码测试通过后feature分支会合并进dev分支，进行下一功能的开发。

