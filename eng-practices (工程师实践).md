# eng-practices (工程师实践)

> Google`s Engineering Practices documentaion （谷歌工程师实践文档）

## The Standard of Code Review (代码审阅标准)

- The primary purpose of code review is to make sure that the overall code health of Google’s code base is improving over time. All of the tools and processes of code review are designed to this end.
- 代码审阅的目的是让谷歌代码仓库的整体代码良好情况随着时间的推移而进一步优化。代码审视的所有工具和流程都是为此去设计的
- In order to accomplish this, a series of trade-offs have to be balanced.
- 为了达成这个目标，一系列的权衡都要被平衡
- First, developers must be able to *make progress* on their tasks. If you never submit an improvement to the codebase, then the codebase never improves. Also, if a reviewer makes it very difficult for *any* change to go in, then developers are disincentivized to make improvements in the future.
- 第一，开发者必须有能力在他们的任务下取得一定的进展，如果你从来没有向代码仓提交过任何改进类的代码，代码库质量将永远不会提高。同时，如果一个审阅代码者对于代码很难进行修改，那么开发者也没有动力去做任何的改进。
- On the other hand, it is the duty of the reviewer to make sure that each CL is of such a quality that the overall code health of their codebase is not decreasing as time goes on. This can be tricky, because often, codebases degrade through small decreases in code health over time, especially when a team is under significant time constraints and they feel that they have to take shortcuts in order to accomplish their goals.
- 另一方面，代码审阅者有责任要确保每一个代码仓库变更列表质量在高水平以上，以保持随着时间推移代码仓库质量不会下降。虽然这可能比较棘手，但是代码仓确实会因为长期一些细小的代码质量下降而降级，特别是一个团队对于时间管理不够重视时，他们会觉得自己不得不使用一些小手段(走捷径)来达成他们的目标。
- Also, a reviewer has ownership and responsibility over the code they are reviewing. They want to ensure that the codebase stays consistent, maintainable, and all of the other things mentioned in [“What to look for in a code review.”](https://google.github.io/eng-practices/review/reviewer/looking-for.html)
- 同时，一个代码审阅者在审阅的时候要有责任感和主人翁意识，他们要确保代码库保持可维护性和连贯稳定性，以及在["我们想在代码审阅的时候得到什么?"](https://google.github.io/eng-practices/review/reviewer/looking-for.html)提及到的内容
- Thus, we get the following rule as the standard we expect in code reviews:
- 所以，我们需要利用这些规则作为我们代码审阅所期待的标准
- **In general, reviewers should favor approving a CL once it is in a state where it definitely improves the overall code health of the system being worked on, even if the CL isn’t perfect.**

- 一般来说，审阅者需要选出一个changeList（通常可表示为一个个PR组成的列表），这个人能扛起整体代码质量推进的大旗，即使它本身并不是最优秀的

- That is *the* senior principle among all of the code review guidelines.

- 以下是围绕代码审阅指导手册的高级准则

- There are limitations to this, of course. For example, if a CL adds a feature that the reviewer doesn’t want in their system, then the reviewer can certainly deny approval even if the code is well-designed.

- 准则中也有一些限制，比如：如果一个变更列表中添加了一些新特性到系统里面，但是审阅者不认可这个新特性，即使代码被精心设计，代码审阅者有权利否认特性的添加，不让新特性合进分支中。

- A key point here is that there is no such thing as “perfect” code—there is only *better* code. Reviewers should not require the author to polish every tiny piece of a CL before granting approval. Rather, the reviewer should balance out the need to make forward progress compared to the importance of the changes they are suggesting. Instead of seeking perfection, what a reviewer should seek is *continuous improvement*. A CL that, as a whole, improves the maintainability, readability, and understandability of the system shouldn’t be delayed for days or weeks because it isn’t “perfect.”

- 一个关键点：不存在完美的代码，只有更好的代码。审阅者不需要要求开发此段代码的owner对每一段代码精雕细琢才能支持合并。对比变更列表的重要性和代码推进的必要性，审阅者需要权衡二者的优先级。审阅者需要做的是持续的提升代码质量而不是代码的完美。对于变更列表来说，提高系统的可维护性、可读性、易懂性刻不容缓，因为代码本身不是完美的。

- Reviewers should *always* feel free to leave comments expressing that something could be better, but if it’s not very important, prefix it with something like “Nit: “ to let the author know that it’s just a point of polish that they could choose to ignore.

- 审阅者应该要做到为了提高代码质量大胆留下评论，不过如果不是很重要的评论，比如修复一些形如："Nit（Nit-pick: 非常细小的描述，形如吹毛求疵)", 这些细致的打磨修复可以选择性忽略。

- Note: Nothing in this document justifies checking in CLs that definitely *worsen* the overall code health of the system. The only time you would do that would be in an [emergency](https://google.github.io/eng-practices/review/emergencies.html).

- 标注：文档中没有任何内容关于检查变更列表对整体代码质量降低的定论，只有在[紧急情况]((https://google.github.io/eng-practices/review/emergencies.html)下才会这样做。

  

- ## Mentoring

- ## 代码监控

- Code review can have an important function of teaching developers something new about a language, a framework, or general software design principles. It’s always fine to leave comments that help a developer learn something new. Sharing knowledge is part of improving the code health of a system over time. Just keep in mind that if your comment is purely educational, but not critical to meeting the standards described in this document, prefix it with “Nit: “ or otherwise indicate that it’s not mandatory for the author to resolve it in this CL.

- 代码审阅应该要有一套重要范式来指导开发者学到新的关于语言，框架，或者常规的软件设计准则。留下review评论帮助开发者学到更多的知识总归是好事，分享知识是是改善系统整体代码质量的重要一环。谨记如果你的review评论是纯教育意义的，满足文档描述的标准但并不重要，可以加上Nit之类的前缀，让作者知道这只是一个细致的优化点，可以忽略掉。

- ## Principles

- ## 准则

- Technical facts and data overrule opinions and personal preferences.

- 技术和数据论据凌驾于意见和偏见之上

- On matters of style, the [style guide](http://google.github.io/styleguide/) is the absolute authority. Any purely style point (whitespace, etc.) that is not in the style guide is a matter of personal preference. The style should be consistent with what is there. If there is no previous style, accept the author’s.

- 风格上的问题，[风格指南](http://google.github.io/styleguide/)是绝对权威，任何纯风格问题(空格等等)只是个人行为，不属于代码风格的范畴，风格应该与风格指南保持一致，如果没有过往的风格限制，请按照开发者个人的去做。

- **Aspects of software design are almost never a pure style issue or just a personal preference.** They are based on underlying principles and should be weighed on those principles, not simply by personal opinion. Sometimes there are a few valid options. If the author can demonstrate (either through data or based on solid engineering principles) that several approaches are equally valid, then the reviewer should accept the preference of the author. Otherwise the choice is dictated by standard principles of software design.

- 软件设计层上从来不是纯风格问题或者仅仅是开发者个人行为问题。他是建立在底层准则之上并且必须以这些准则作为根基，不是简单的认为是个人观点。即使有时候有不少有效的论点。如果作者可以证明(绝对的数据或者建立在软件工程坚实的准则)几种方法同样是奏效的，然后审阅者应该接受开发者个人的行为喜好，否则，选择权应该建立在标准的软件设计准则上。

- If no other rule applies, then the reviewer may ask the author to be consistent with what is in the current codebase, as long as that doesn’t worsen the overall code health of the system.

- 同样的没有其他应用的原则，只要使系统代码质量不下降，审阅者可以要求开发者风格按照现有代码库保持一致。

- ## Resolving Conflicts

- ## 解决冲突

- In any conflict on a code review, the first step should always be for the developer and reviewer to try to come to consensus, based on the contents of this document and the other documents in [The CL Author’s Guide](https://google.github.io/eng-practices/review/developer/) and this [Reviewer Guide](https://google.github.io/eng-practices/review/reviewer/).

- 任何代码审计出现的冲突，第一步永远应该是开发者和审阅者根据[变更列表作者指南](https://google.github.io/eng-practices/review/developer/)或者[审阅者指南](https://google.github.io/eng-practices/review/reviewer/)一起达成共识

- When coming to consensus becomes especially difficult, it can help to have a face-to-face meeting or a video conference between the reviewer and the author, instead of just trying to resolve the conflict through code review comments. (If you do this, though, make sure to record the results of the discussion as a comment on the CL, for future readers.)

- 遇到共识进度推进十分困难的时候，一次开发者和审阅者面对面会议或者视频会议能推进共识的达成，而不是仅靠审阅提出的评论去解决冲突(确保这种做法后留下一个会议讨论结果作为变更列表中的评论，给以后的阅读者看)

- If that doesn’t resolve the situation, the most common way to resolve it would be to escalate. Often the escalation path is to a broader team discussion, having a Technical Lead weigh in, asking for a decision from a maintainer of the code, or asking an Eng Manager to help out. **Don’t let a CL sit around because the author and the reviewer can’t come to an agreement.**

- 如果还是解决不了问题，常见的方法是会议升级，通常可以进行更宽泛的团队会议讨论，让技术Leader参与进来，让代码的维护者做这个决定，或者请求技术经理帮忙解决。**不要让变更列表由于作者和审阅人无法得出一个解决方案而一直搁置审阅**



### 下一篇： [我在代码审阅中想收获到什么东西]()

