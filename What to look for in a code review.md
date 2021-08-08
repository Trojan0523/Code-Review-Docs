# What to look for in a code review

# 代码审阅中我想得到什么

- Note: Always make sure to take into account [The Standard of Code Review](https://google.github.io/eng-practices/review/reviewer/standard.html) when considering each of these points.
- 标注：考虑任何观点之前，必须充分考虑[代码审阅标准](https://github.com/Trojan0523/Code-Review-Docs/blob/main/eng-practices%20(%E5%B7%A5%E7%A8%8B%E5%B8%88%E5%AE%9E%E8%B7%B5).md)

## Design

## 设计

- The most important thing to cover in a review is the overall design of the CL. Do the interactions of various pieces of code in the CL make sense? Does this change belong in your codebase, or in a library? Does it integrate well with the rest of your system? Is now a good time to add this functionality?
- 审查中最重要的部分应该是变更列表的整体设计。变更列表里面的各个代码块的交互是否有意义？这段变更在你的代码仓，还是库中？对于系统的其他部分，你的代码是否得到良好的集成方式？添加这段功能是最好时机吗？

## Functionality

## 功能

- Does this CL do what the developer intended? Is what the developer intended good for the users of this code? The “users” are usually both end-users (when they are affected by the change) and developers (who will have to “use” this code in the future).
- 变更列表中的变更是否符合开发者的想法？开发者的想法是否对使用此段代码的开发者有益？"用户"通常包含端对端用户(当受最终代码变更影响时)和开发者(将来会使用这段代码的人)
- Mostly, we expect developers to test CLs well-enough that they work correctly by the time they get to code review. However, as the reviewer you should still be thinking about edge cases, looking for concurrency problems, trying to think like a user, and making sure that there are no bugs that you see just by reading the code.
- 大多数情况下，我们期待开发者能很好的测试自己的变更，以便审阅者能够将审阅工作正常开展下去。然而，作为一个开发者，对于边界情况仍然要多思考，找出并发问题，尝试站在用户(使用方开发者)角度思考，确保**所见即所得**，减少bug率.
- You *can* validate the CL if you want—the time when it’s most important for a reviewer to check a CL’s behavior is when it has a user-facing impact, such as a **UI change**. It’s hard to understand how some changes will impact a user when you’re just reading the code. For changes like that, you can have the developer give you a demo of the functionality if it’s too inconvenient to patch in the CL and try it yourself.
- 有需要的时候，你自己也可以验证变更提交，当出现面向用户(比如用户界面变更)影响时，审阅者最重要的任务就是检查变更行为，阅读这些代码的时候，是比较难了解有些变更可能会影响用户使用的，对于这些变更，如果变更中不好去做修复的话，你可以让开发者给你一个这个功能的Demo做演示并且自己尝试修复。
- Another time when it’s particularly important to think about functionality during a code review is if there is some sort of **parallel programming** going on in the CL that could theoretically cause deadlocks or race conditions. These sorts of issues are very hard to detect by just running the code and usually need somebody (both the developer and the reviewer) to think through them carefully to be sure that problems aren’t being introduced. (Note that this is also a good reason not to use concurrency models where race conditions or deadlocks are possible—it can make it very complex to do code reviews or understand the code.)
- 另一方面，代码审阅期间如果变更中存在某种并发编程造成的竞态或死锁问题时，对于功能的思考显得尤为重要。这一类的问题比较难仅通过跑下代码检测出来，通常需要(开发者和审阅者)细致查看才能确保不会引入问题。(同时存在一种原因是：当竞态和死锁问题可能存在时，不要使用并发模型，因为这可能导致代码审阅或者理解代码本身存在一定的复杂度)。

## Complexity

## 复杂度

- Is the CL more complex than it should be? Check this at every level of the CL—are individual lines too complex? Are functions too complex? Are classes too complex? “Too complex” usually means **“can’t be understood quickly by code readers.”** It can also mean **“developers are likely to introduce bugs when they try to call or modify this code.”**
- 变更本身就比设想的要复杂？任何级别的变更都要进行检查 -- 个人代码是否过于复杂？功能是否过于复杂？类过于复杂？过于复杂通常意味着不能被代码阅读者快速理解。也意味着开发者有可能在调用或者修改这些代码的时候存在bug。
- A particular type of complexity is **over-engineering**, where developers have made the code more generic than it needs to be, or added functionality that isn’t presently needed by the system. Reviewers should be especially vigilant about over-engineering. Encourage developers to solve the problem they know needs to be solved *now*, not the problem that the developer speculates *might* need to be solved in the future. The future problem should be solved once it arrives and you can see its actual shape and requirements in the physical universe.
- 一种特别的复杂度叫做："过度设计" ，开发者将代码封装的比其自身更加具有通用性，或者添加一些系统目前不需要使用的功能。审阅者需要对过度设计更加谨慎，鼓励开发者关注解决当前问题而不是超前设计。将来会出现的问题只有在个人发现或者需求提出的时候才需要去解决。

## Tests

## 测试

- Ask for unit, integration, or end-to-end tests as appropriate for the change. In general, tests should be added in the same CL as the production code unless the CL is handling an [emergency](https://google.github.io/eng-practices/review/emergencies.html).
- 做合适的变更单元、集成、或者端对端测试。实际上，测试也应该跟生产代码一起放入变更中，除非变更是比较紧急上线的(hotfix)
- Make sure that the tests in the CL are correct, sensible, and useful. Tests do not test themselves, and we rarely write tests for our tests—a human must ensure that tests are valid.
- 确保变更中的测试是正确的，合理的，有用的。测试不能测试其自身，我们也基本不会给我们的测试写测试，所以要保证测试是有效的
- Will the tests actually fail when the code is broken? If the code changes beneath them, will they start producing false positives? Does each test make simple and useful assertions? Are the tests separated appropriately between different test methods?
- 代码出现问题的时候测试也会出现失败用例吗？如果代码变更是以测试为基座的，测试也会出现同样的结果吗？每个测试是否保持简单和可用断言? 不同的测试用例能适当的覆盖分支吗？
- Remember that tests are also code that has to be maintained. Don’t accept complexity in tests just because they aren’t part of the main binary.
- 记住测试也是代码，也需要被维护。不能因为其不是主分支的一部分而接受过于复杂的测试用例

## Naming

## 命名规范

- Did the developer pick good names for everything? A good name is long enough to fully communicate what the item is or does, without being so long that it becomes hard to read.
- 开发者有对所有代码赋予一个良好的命名吗？一个好的命名是足够长去充分表达目标项是是啥或者做啥的，命名不够充分会导致比较难阅读

## Comments

## 注释

- Did the developer write clear comments in understandable English? Are all of the comments actually necessary? Usually comments are useful when they **explain why** some code exists, and should not be explaining *what* some code is doing. If the code isn’t clear enough to explain itself, then the code should be made simpler. There are some exceptions (regular expressions and complex algorithms often benefit greatly from comments that explain what they’re doing, for example) but mostly comments are for information that the code itself can’t possibly contain, like the reasoning behind a decision.
- 开发者可以用可理解的英语写清晰的注释吗?是否所有注释都是必须的？通常注释只适用于解释代码存在的合理性而不是解释代码在做什么。如果代码不够清晰去解释自身的话，代码需要尽可能保持更简单。不过还是存在一些例外(举例：正则表达式，复杂算法经常能从解释用法的注释中得到启发)。但是大多数注释用于代码本身不可能包含的信息，例如决策背后的原理
- It can also be helpful to look at comments that were there before this CL. Maybe there is a TODO that can be removed now, a comment advising against this change being made, etc.
- 查看变更前的评论也很重要，现在有一个待办项可以删掉，但是不要删除变更后的评论
- Note that comments are different from *documentation* of classes, modules, or functions, which should instead express the purpose of a piece of code, how it should be used, and how it behaves when used.
- 前面的注释有可能跟文档中类、模块、函数有出入，这类注释需要保持代码表达的意图、代码应该怎么被使用、还有在使用时功能的行为。

## Style

## 风格

- We have [style guides](http://google.github.io/styleguide/) at Google for all of our major languages, and even for most of the minor languages. Make sure the CL follows the appropriate style guides.
- 谷歌内部对于主力开发语言和次要语言都有着全覆盖的[代码风格指南](http://google.github.io/styleguide/) ，确保变更中的代码都要遵循合适的开发风格指南
- If you want to improve some style point that isn’t in the style guide, prefix your comment with “Nit:” to let the developer know that it’s a nitpick that you think would improve the code but isn’t mandatory. Don’t block CLs from being submitted based only on personal style preferences.
- 如果你想改进不在风格指南中的某些代码风格点，请以前缀"Nit(润色):  "让开发者知道这是一个你想改进但并不强制的润色点。不要让这些带有个人风格偏好的变更使整个提交处于一个停滞的状态。
- The author of the CL should not include major style changes combined with other changes. It makes it hard to see what is being changed in the CL, makes merges and rollbacks more complex, and causes other problems. For example, if the author wants to reformat the whole file, have them send you just the reformatting as one CL, and then send another CL with their functional changes after that.
- 作者的变更不应该在一个主要风格的变更中混合其他的修改，这会导致变更审阅难度加大，让合并代码和回滚代码变得更加复杂或者导致其他问题出现。举例：如果作者想对整个文件做格式化，一个变更中应该只能有格式化的内容，其他对于功能的修改应该写在其他的变更中。

## Consistency

## 一致性

- What if the existing code is inconsistent with the style guide? Per our [code review principles](https://google.github.io/eng-practices/review/reviewer/standard.html#principles), the style guide is the absolute authority: if something is required by the style guide, the CL should follow the guidelines.
- 如果现有代码跟风格指南的不一致怎么办？根据[代码审阅原则](),风格指南是绝对权威，如果对风格指南有要求，那么变更就应该遵循指南去走。
- In some cases, the style guide makes recommendations rather than declaring requirements. In these cases, it’s a judgment call whether the new code should be consistent with the recommendations or the surrounding code. Bias towards following the style guide unless the local inconsistency would be too confusing.
- 某些情况中，风格指南是建议性指导而不是明确要求。这些情况需要判断新代码需不需要与已有代码风格保持一致，通常是偏于与风格指南保持一致，不然局部不一致会导致整体风格过于混乱
- If no other rule applies, the author should maintain consistency with the existing code.
- 如果没有其他规则应用，作者应该保持写入修改与现有代码保持风格一致
- Either way, encourage the author to file a bug and add a TODO for cleaning up existing code.
- 同样，鼓励作者以bug fix的形式去整理已有的代码

## Documentation

## 文档

- If a CL changes how users build, test, interact with, or release code, check to see that it also updates associated documentation, including READMEs, g3doc pages, and any generated reference docs. If the CL deletes or deprecates code, consider whether the documentation should also be deleted. If documentation is missing, ask for it.
- 如果一个变更需要使用者测试、写交互行为、或者发布代码，则需要检查文档是否需要协同更新。包含README， g3doc pages,或者常规的行为文档。如果变更中删除或者弃用代码，请考虑清楚文档是否需要删除，如果文档缺失，请补全。

## Every Line

## 每一行代码变更

- In the general case, look at *every* line of code that you have been assigned to review. Some things like data files, generated code, or large data structures you can scan over sometimes, but don’t scan over a human-written class, function, or block of code and assume that what’s inside of it is okay. Obviously some code deserves more careful scrutiny than other code—that’s a judgment call that you have to make—but you should at least be sure that you *understand* what all the code is doing.
- 常规场景中，每一行代码都需要做代码审视，一些像数据文件，生成的代码，或者巨量数据通常只需要扫视一眼即可，但是人为编写的类，函数、代码块或者是认为可靠的代码都不能粗略一眼带过。特别是一些比其他代码更需要仔细审视的代码，有些权衡就必须要考虑，但是起码得保证你能知道所有的代码是怎么运行的
- If it’s too hard for you to read the code and this is slowing down the review, then you should let the developer know that and wait for them to clarify it before you try to review it. At Google, we hire great software engineers, and you are one of them. If you can’t understand the code, it’s very likely that other developers won’t either. So you’re also helping future developers understand this code, when you ask the developer to clarify it.
- 如果在阅读代码的时候比较困难同时审阅的速度在下降的话，这时候需要让开发者知道这一点并且让他们把代码结构整理清晰后再做审阅。谷歌的做法是，招一些比较出色的软件工程师。如果你看不懂这些代码，有可能其他开发者也看不懂，所以你要做的是帮助以后的开发者扫清前面的障碍，能流畅阅读代码。
- If you understand the code but you don’t feel qualified to do some part of the review, [make sure there is a reviewer](https://google.github.io/eng-practices/review/reviewer/looking-for.html#every-line-exceptions) on the CL who is qualified, particularly for complex issues such as security, concurrency, accessibility, internationalization, etc.
- 虽然你能理解这些代码，但是对于某些部分的审视不是特别满意，[变更列表中有一位合格的审阅者](https://google.github.io/eng-practices/review/reviewer/looking-for.html#every-line-exceptions) ，特别是对于复杂性较强的问题(安全性，一致性，访问性，国际化等等)

### Exceptions

### 异常

- What if it doesn’t make sense for you to review every line? For example, you are one of multiple reviewers on a CL and may be asked:

- 如果审视到的代码都没有意义怎么办？例如：你是众多审阅者其中一员，有可能被问到：
  - To review only certain files that are part of a larger change.
  - 仅审查较大变更的文件
  - To review only certain aspects of the CL, such as the high-level design, security implications, etc.
  - 仅审查变更列表里面某些方面的代码，例如高阶设计，安全影响等等
- In these cases, note in a comment which parts you reviewed. Prefer giving [LGTM with comments](https://google.github.io/eng-practices/review/reviewer/speed.html#lgtm-with-comments) .
- 在这些情况下，可以将你审阅的部分记录下一个评论，具体请看:  [代码已经Review过了，可以合并](https://google.github.io/eng-practices/review/reviewer/speed.html#lgtm-with-comments) .

- If you instead wish to grant LGTM after confirming that other reviewers have reviewed other parts of the CL, note this explicitly in a comment to set expectations. Aim to [respond quickly](https://google.github.io/eng-practices/review/reviewer/speed.html#responses) once the CL has reached the desired state.
- 如果确认其他审阅者已经审阅完其他部分的变更并且想给与合并支持，请留下一个明确的评论以表明你的合并期望值，以达到[快速响应](https://google.github.io/eng-practices/review/reviewer/speed.html#responses)合并的目的

## Context

## 上下文

- It is often helpful to look at the CL in a broad context. Usually the code review tool will only show you a few lines of code around the parts that are being changed. Sometimes you have to look at the whole file to be sure that the change actually makes sense. For example, you might see only four new lines being added, but when you look at the whole file, you see those four lines are in a 50-line method that now really needs to be broken up into smaller methods.
- 宽泛的上下文对于查看变更有着很大的帮助。通常代码审视工具只会展示修改过的部分行代码，有时你需要查看整个文件确保整个修改是起作用的。例如：审阅者查看四行新增的代码，但是当你在看整个文件的时候，你会发现这四行在一个五十行的方法里面，并且整个方法需要拆分成数个更细颗粒度的方法。
- It’s also useful to think about the CL in the context of the system as a whole. Is this CL improving the code health of the system or is it making the whole system more complex, less tested, etc.? **Don’t accept CLs that degrade the code health of the system.** Most systems become complex through many small changes that add up, so it’s important to prevent even small complexities in new changes.
- 从整个系统的上下文中去思考变更也是很有帮助的。此变更是否对整个系统的代码质量有帮助？或者造成整个系统的复杂度增强，更少的测试等等？不能接受变更带来的代码质量下降。大多数系统会通过几个小的变更变得愈发复杂，避免新变更带来的复杂度上升这一点很重要。

## Good Things

## 值得支持的变更

- If you see something nice in the CL, tell the developer, especially when they addressed one of your comments in a great way. Code reviews often just focus on mistakes, but they should offer encouragement and appreciation for good practices, as well. It’s sometimes even more valuable, in terms of mentoring, to tell a developer what they did right than to tell them what they did wrong.
- 如果在变更审阅的时候看到不错的地方，务必要告诉开发者，特别是他们以一个不错的方式解决了一个自己留下的评论时。代码审阅通常仅关注于错误，但是他们的优秀实践也应该被充分赋予鼓励和欣赏。有时告诉开发者做的好的地方比告诉他们做的不足的地方效果更好~

## Summary

## 总结

- In doing a code review, you should make sure that:
- 做代码审查的时候，应该确保：
- The code is well-designed.
- 代码是精心设计的
- The functionality is good for the users of the code.
- 此功能评论应该是对用户的代码有好处的
- Any UI changes are sensible and look good.
- 任何的用户界面修改都应该是有意义的
- Any parallel programming is done safely.
- 任何并发编程都做不到安全至上
- The code isn’t more complex than it needs to be.
- 代码不能比其本身的需求更复杂
- The developer isn’t implementing things they *might* need in the future but don’t know they need now.
- 开发者不应该添加现在用不上但是将来可能会用到的东西
- Code has appropriate unit tests.
- 审阅的代码要上单元测试，要能被测试
- Tests are well-designed.
- 测试也要精心设计
- The developer used clear names for everything.
- 任何命名都必须是清晰的
- Comments are clear and useful, and mostly explain *why* instead of *what*.
- 注释必须清晰有效，大部分只是解释为什么或者做了什么
- Code is appropriately documented (generally in g3doc).
- 代码应该适当留下文档
- The code conforms to our style guides.
- 代码应该符合团队自身的代码风格



- Make sure to review **every line** of code you’ve been asked to review, look at the **context**, make sure you’re **improving code health**, and compliment developers on **good things** that they do.

- 确保审阅每一行要求审查的代码，回顾其上下文，确保你在改进整体代码质量，同时要对于开发者做的好的地方也要提出赞扬。

  

## 下一篇：指路[代码审阅](https://github.com/Trojan0523/Code-Review-Docs/blob/main/Navigating%20a%20CL%20in%20review.md)

