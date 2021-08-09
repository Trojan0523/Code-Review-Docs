# Speed of Code Reviews

# 代码审阅时效

## Why Should Code Reviews Be Fast?

## 为什么代码审阅需要快速完成？

- **At Google, we optimize for the speed at which a team of developers can produce a product together**, as opposed to optimizing for the speed at which an individual developer can write code. The speed of individual development is important, it’s just not *as* important as the velocity of the entire team.
- 在谷歌，我们针对一个团队开发者产出的产品一起去进行时速优化，而不是针对一个个体开发者写的代码做的优化。开发者个人的速度是很重要，但是没有整个团队的速度的重要性高。
- When code reviews are slow, several things happen:
- 代码审阅速度慢的时候，有些情况就会发生：
  - **The velocity of the team as a whole is decreased.** Yes, the individual, who doesn’t respond quickly to the review, gets other work done. However, new features and bug fixes for the rest of the team are delayed by days, weeks, or months as each CL waits for review and re-review.
  - 整个团队的速度会下降。个体的代码审阅的确不会很快得到回应，得等其他工作做完才会一并提交。然而变更中剩下的新特性和bug修复也会顺带这延后个数天、数周或者数月。
  - **Developers start to protest the code review process.** If a reviewer only responds every few days, but requests major changes to the CL each time, that can be frustrating and difficult for developers. Often, this is expressed as complaints about how “strict” the reviewer is being. If the reviewer requests the *same* substantial changes (changes which really do improve code health) but responds *quickly* every time the developer makes an update, the complaints tend to disappear. **Most complaints about the code review process are actually resolved by making the process faster.**
  - 开发者对于代码审阅流程开始抗议，如果一个审阅者每隔几天才做一次回应，但是请求变更在变更列表又十分重要，这种情况反而另开发者十分困惑和沮丧。通常这是审阅者的严格带来的抱怨。如果审阅者要求的重大变动(变动确实能改进代码质量)，开发者每次都能迅速做出回应，那这些抱怨就会随风消失。大多数对于代码审阅流程的抱怨都能通过加快代码流程解决。
  - **Code health can be impacted.** When reviews are slow, there is increased pressure to allow developers to submit CLs that are not as good as they could be. Slow reviews also discourage code cleanups, refactorings, and further improvements to existing CLs.
  - 代码质量能被影响。审阅进度很慢的时候，压力就会增加，从而允许开发者提交低质量的变更。低速的审阅也不利于代码的整理，重构和现有变更的进一步提升。

## How Fast Should Code Reviews Be?

## 代码审阅的速度应该怎么权衡？

- If you are not in the middle of a focused task, **you should do a code review shortly after it comes in.**
- 如果手中的任务不是特别的紧，你应该在接到代码审阅任务后做一个快速的代码审阅
- **One business day is the maximum time it should take to respond** to a code review request (i.e. first thing the next morning).
- 工作日是最好的时间，这个时间代码审阅请求应该被快速相应(第二天早上第一时间)
- Following these guidelines means that a typical CL should get multiple rounds of review (if needed) within a single day.
- 按照指南上的说法，一个典型的变更需要在同一天有需要的情况下进行多次的审阅

## Speed vs. Interruption

## 时效 VS 干扰

- There is one time where the consideration of personal velocity trumps team velocity. **If you are in the middle of a focused task, such as writing code, don’t interrupt yourself to do a code review.** Research has shown that it can take a long time for a developer to get back into a smooth flow of development after being interrupted. So interrupting yourself while coding is actually *more* expensive to the team than making another developer wait a bit for a code review.
- 有时候，个人速度比团队速度要重要不少。比如沉迷写码的时候，就不要打断自己去做代码审阅了。研究表明被打断后开发者需要花大量的时间才能回到流畅的工作流中去。所以打断自己的开发在团队中的成本比稍微延迟一会做代码审阅要高得多。
- Instead, wait for a break point in your work before you respond to a request for review. This could be when your current coding task is completed, after lunch, returning from a meeting, coming back from the breakroom, etc.
- 相反，在代码请求审阅之前，你需要留有一个时间点给自己做缓冲，可以是现有工作完成的时候，吃完饭，开完会，又或者是结束休息后。

## Fast Responses

## 快速相应

- When we talk about the speed of code reviews, it is the *response* time that we are concerned with, as opposed to how long it takes a CL to get through the whole review and be submitted. The whole process should also be fast, ideally, but **it’s even more important for the \*individual responses\* to come quickly than it is for the whole process to happen rapidly.**
- 谈及代码审阅时效时，响应时间往往是我们最关心的，而不是整个变更审阅并提交的时间。理想状态下整个流程应该是很快的，不过往往是一些个人审阅的回应比整个流程要响应的更加迅速。
- Even if it sometimes takes a long time to get through the entire review *process*, having quick responses from the reviewer throughout the process significantly eases the frustration developers can feel with “slow” code reviews.
- 即使有时候需要花费大量时间完成整个审阅流程，开发者如果对流程中影响较大的情况的慢审阅感到进度受阻时，也需要加快响应速度。
- If you are too busy to do a full review on a CL when it comes in, you can still send a quick response that lets the developer know when you will get to it, suggest other reviewers who might be able to respond more quickly, or [provide some initial broad comments](https://google.github.io/eng-practices/review/reviewer/navigate.html). (Note: none of this means you should interrupt coding even to send a response like this—send the response at a reasonable break point in your work.)
- 太忙没办法完成一个完整的审阅时，你也要给开发者一个快速的回应，告诉他你以后会做这个审阅，也可以向其他有能力去快速响应请求的审阅者求助，或者[提供一些简单的评论](https://google.github.io/eng-practices/review/reviewer/navigate.html)(注意：上面没有一项注释是强调你应该停下手中的开发去做回应，可以在工作中留下一个空出的时间点来做回应)
- **It is important that reviewers spend enough time on review that they are certain their “LGTM” means “this code meets [our standards](https://google.github.io/eng-practices/review/reviewer/standard.html).”** However, individual responses should still ideally be [fast](https://google.github.io/eng-practices/review/reviewer/speed.html#fast).
- 审阅者留下足够的时间在审阅中并确保代码已经审阅过，可以合并(LGTM: looks goods to me,谷歌俚语，已经review过，可以合并)，这很重要，表明审阅的代码已经达到[我们的标准](https://google.github.io/eng-practices/review/reviewer/standard.html).然而，来自开发者个人的询问都应该保持快速相应。

## Cross-Time-Zone Reviews

## 跨时区审阅

- When dealing with time zone differences, try to get back to the author when they are still in the office. If they have already gone home, then try to make sure your review is done before they get back to the office the next day.
- 处理不同时区的审阅时，问问作者是不是已经下班了，如果他们已经下班，尝试确保第二天作者上班之前能完成审阅。

## LGTM With Comments

## 审阅后的可合并评论

- In order to speed up code reviews, there are certain situations in which a reviewer should give LGTM/Approval even though they are also leaving unresolved comments on the CL. This is done when either:
- 为了给代码审阅提速，有几种情况可以支持合并代码，即使他们在变更列表中还没解决完建议修改项，符合下面几项的都可以：
  - The reviewer is confident that the developer will appropriately address all the reviewer’s remaining comments.
  - 开发者给与审阅者信心，保证能适当的完成所有审阅者提出的评论修改点。
  - The remaining changes are minor and don’t *have* to be done by the developer.
  - 剩下的变更是次要的，不强迫开发者做完所有的修改
- The reviewer should specify which of these options they intend, if it is not otherwise clear.
- 审阅者应该挑出哪些选项是他们打算做的，否则开发者对于哪些需要完成的修改没有清晰的认识
- LGTM With Comments is especially worth considering when the developer and reviewer are in different time zones and otherwise the developer would be waiting for a whole day just to get “LGTM, Approval.”
- 当开发者和审阅者不在同一个时区的时候，可以合并的评论提示尤其需要深思熟虑，不然开发者需要为了一个支持合并的评论而等上个一整天，太浪费时间。

## Large CLs

## 巨大变更

- If somebody sends you a code review that is so large you’re not sure when you will be able to have time to review it, your typical response should be to ask the developer to [split the CL into several smaller CLs](https://google.github.io/eng-practices/review/developer/small-cls.html) that build on each other, instead of one huge CL that has to be reviewed all at once. This is usually possible and very helpful to reviewers, even if it takes additional work from the developer.
- 当开发者做了一个比较大的代码变更审阅请求，你不确保有没有足够的时间去做审阅时，典型的回应应该是让开发者拆分变更，拆成几个小的变更，而不是每次审阅一个很大的变更。虽然给开发者带来额外的工作，但是这通常有助于审阅者做更好的审阅。
- If a CL *can’t* be broken up into smaller CLs, and you don’t have time to review the entire thing quickly, then at least write some comments on the overall design of the CL and send it back to the developer for improvement. One of your goals as a reviewer should be to always unblock the developer or enable them to take some sort of further action quickly, without sacrificing code health to do so.
- 如果这个变更还是没有办法做拆分，同时你也没时间对整个变更做审阅，这时候最起码对于整个变更设计留下一些评论让开发者去做改进。审阅者的其中一个目的就是解放开发者并且让他们短期内做出一些改进，而不是一味牺牲代码质量。

## Code Review Improvements Over Time

## 代码审阅无时无刻都在改进代码质量

- If you follow these guidelines and you are strict with your code reviews, you should find that the entire code review process tends to go faster and faster over time. Developers learn what is required for healthy code, and send you CLs that are great from the start, requiring less and less review time. Reviewers learn to respond quickly and not add unnecessary latency into the review process. But **don’t compromise on the [code review standards](https://google.github.io/eng-practices/review/reviewer/standard.html) or quality for an imagined improvement in velocity**—it’s not actually going to make anything happen more quickly, in the long run.
- 跟着指南走，严格要求代码审阅，你会发现无时无刻代码审阅流程都要加快。开发者需要在如何保证代码质量中学会改进自己的代码，发给审阅者的代码变更都要比一开始的要好，然后不断缩短审阅时间。审阅者也应该学会快速响应，同时不要在审阅流程中添乱。但是也不要为了想象中的速度提高而在代码审阅标准中做出让步，从长远的角度来看，这不会对任何东西增速。

## Emergencies

## 紧急事件

- There are also [emergencies](https://google.github.io/eng-practices/review/emergencies.html) where CLs must pass through the *whole* review process very quickly, and where the quality guidelines would be relaxed. However, please see [What Is An Emergency?](https://google.github.io/eng-practices/review/emergencies.html#what) for a description of which situations actually qualify as emergencies and which don’t.
- 有些紧急事件，变更必须快速通过整个审查流程，同时也要对质量标准做出让步。不过这种情况需要参考[什么是紧急事件?](https://google.github.io/eng-practices/review/emergencies.html#what)，里面介绍了符合和不符合紧急情况的描述。



## 下一篇： [如何编写代码审阅评论](https://github.com/Trojan0523/Code-Review-Docs/blob/main/How%20to%20write%20code%20review.md)



