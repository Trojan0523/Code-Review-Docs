# How to write code review

# 如何撰写一个代码审阅评论

## Summary

## 总结

- Be kind.
- 友好
- Explain your reasoning.
- 解释清楚你的论点
- Balance giving explicit directions with just pointing out problems and letting the developer decide.
- 单纯指出问题和给出一个明确的方向二者要做平衡，不要让开发者自己做选择。
- Encourage developers to simplify code or add code comments instead of just explaining the complexity to you.
- 鼓励开发者去简化自己的代码，增加更多的注释，而不是向审阅者去解释其中的复杂度

## Courtesy

## 礼貌

- In general, it is important to be [courteous and respectful](https://chromium.googlesource.com/chromium/src/+/master/docs/cr_respect.md) while also being very clear and helpful to the developer whose code you are reviewing. One way to do this is to be sure that you are always making comments about the *code* and never making comments about the *developer*. You don’t always have to follow this practice, but you should definitely use it when saying something that might otherwise be upsetting or contentious. For example:
- 通常，在代码审阅期间，给予开发者足够的[礼貌和尊重](https://chromium.googlesource.com/chromium/src/+/master/docs/cr_respect.md)也很重要，这也能使他们的代码写的更加清晰。其中一种方式就是永远只对代码做评论而不对他人做评论。不需要总是按照实践的方式去做,不过在谈及一些会令人感到不高兴或者不理解的事情时，此实践必须要使用，举例：
- Bad: “Why did **you** use threads here when there’s obviously no benefit to be gained from concurrency?”
- 做的不好的：为什么你要在这大量的使用对并发完全没有帮助的线程？
- Good: “The concurrency model here is adding complexity to the system without any actual performance benefit that I can see. Because there’s no performance benefit, it’s best for this code to be single-threaded instead of using multiple threads.”
- 做的好的：这里的并发模型中添加了不少复杂的东西，我没有在系统的发现实际的性能好处。这里没有带来性能的优化，对于这段代码最好是使用单线程而不是使用多线程的的形式。

## Explain Why

## 解释清楚为什么

- One thing you’ll notice about the “good” example from above is that it helps the developer understand *why* you are making your comment. You don’t always need to include this information in your review comments, but sometimes it’s appropriate to give a bit more explanation around your intent, the best practice you’re following, or how your suggestion improves code health.
- 写一些好的例子有助于开发者理解为什么审阅者会留下这样的评论。审阅评论中也不是都需要去这样做，但是有时候对于你的意图留下一些解释、认可的最佳实践、或者怎么去改善代码质量的建议。

## Giving Guidance

## 给与指导

- **In general it is the developer’s responsibility to fix a CL, not the reviewer’s.** You are not required to do detailed design of a solution or write code for the developer.
- 改进变更中的缺陷，通常是开发者的责任而不是审阅者的。你不需要写一个详细设计的解决方案或者给开发者留下代码。
- This doesn’t mean the reviewer should be unhelpful, though. In general you should strike an appropriate balance between pointing out problems and providing direct guidance. Pointing out problems and letting the developer make a decision often helps the developer learn, and makes it easier to do code reviews. It also can result in a better solution, because the developer is closer to the code than the reviewer is.
- 这也不意味着审阅者应该不做帮助。通常你需要平衡指出问题和提供直接的指导二者关系。直接指出问题，让开发者自己做决定通常有助于开发者学到怎么去改进，也能让审阅者的审阅能更好的进行下去。也可以给一个更好的解决方案定论，因为开发者比审阅者更了解代码。
- However, sometimes direct instructions, suggestions, or even code are more helpful. The primary goal of code review is to get the best CL possible. A secondary goal is improving the skills of developers so that they require less and less review over time.
- 有时候，直接的指导，建议甚至是代码更有助于开发者的成长。代码审阅的最主要目的就是尽可能让变更做到最好。次要的目的才是提高开发者的技能，让审阅的次数越来越少。
- Remember that people learn from reinforcement of what they are doing well and not just what they could do better. If you see things you like in the CL, comment on those too! Examples: developer cleaned up a messy algorithm, added exemplary test coverage, or you as the reviewer learned something from the CL. Just as with all comments, include [why](https://google.github.io/eng-practices/review/reviewer/comments.html#why) you liked something, further encouraging the developer to continue good practices.
- 记住一点，开发者需要从他们做的好的地方和需要做的更好的地方得到加强，如果发现变更中你认可的地方，也请留下评论，举例：开发者整理了一个凌乱的算法，添加示例性测试覆盖率，或者作为开发者的你从变更中学到的东西。所有的评论，包含你认可的修改，能鼓励开发者继续去做进一步的最佳实践落地。

## Accepting Explanations

## 接受解释

- If you ask a developer to explain a piece of code that you don’t understand, that should usually result in them **rewriting the code more clearly**. Occasionally, adding a comment in the code is also an appropriate response, as long as it’s not just explaining overly complex code.
- 如果审阅者要求开发者解释这段你看不懂的代码，应该要求开发者更清晰的去重写这段代码，偶尔添加一些注释到代码中区也是一个合适的对应，只要不是单单解释复杂的代码。
- **Explanations written only in the code review tool are not helpful to future code readers.** They are acceptable only in a few circumstances, such as when you are reviewing an area you are not very familiar with and the developer explains something that normal readers of the code would have already known.
- 只通过代码审阅工具写解释不利于以后代码阅读者的阅读。这种做法仅在少数情况下可以接受。比如审阅者在审阅一个不太熟悉的模块时，开发者会解释一些普通阅读者已经知道的内容。



## 下一篇： [处理代码审阅中的阻力]()

