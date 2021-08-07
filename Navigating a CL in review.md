# Navigating a CL in review

# 指路审阅变更

## Summary

## 总结

- Now that you know [what to look for](https://github.com/Trojan0523/Code-Review-Docs/blob/main/%E4%BB%A3%E7%A0%81%E5%AE%A1%E9%98%85%E4%B8%AD%E6%88%91%E6%83%B3%E5%BE%97%E5%88%B0%E4%BB%80%E4%B9%88.md), what’s the most efficient way to manage a review that’s spread across multiple files?

- 现在你已经知道[代码审阅中你想获得什么](https://github.com/Trojan0523/Code-Review-Docs/blob/main/%E4%BB%A3%E7%A0%81%E5%AE%A1%E9%98%85%E4%B8%AD%E6%88%91%E6%83%B3%E5%BE%97%E5%88%B0%E4%BB%80%E4%B9%88.md)，什么是管理分布多个文件的复查最有效率的方式？

  - Does the change make sense? Does it have a good [description](https://google.github.io/eng-practices/review/developer/cl-descriptions.html)?
  - 变更是否有意义，有没有一个良好的描述？
  - Look at the most important part of the change first. Is it well-designed overall?
  - 首先找出变更最重要的一部分。这一块是否被全面精心设计？
  - Look at the rest of the CL in an appropriate sequence.
  - 按适当的顺序查看变更列表中剩余的部分

- ## Step One: Take a broad view of the change

- ## 步骤1： 对于变更有一个全局的认识

- Look at the [CL description](https://google.github.io/eng-practices/review/developer/cl-descriptions.html) and what the CL does in general. Does this change even make sense? If this change shouldn’t have happened in the first place, please respond immediately with an explanation of why the change should not be happening. When you reject a change like this, it’s also a good idea to suggest to the developer what they should have done instead.

- 看看变更[列表描述](https://google.github.io/eng-practices/review/developer/cl-descriptions.html)，了解一下一个变更通常长什么样子。变更是否有存在的意义？如果这个变更不合时宜，请立即留下一个为什么不应该存在的解释作为回应，做这种拒绝变更的时候，告诉开发者应该怎么做也不失为一种好的方法。

- For example, you might say “Looks like you put some good work into this, thanks! However, we’re actually going in the direction of removing the FooWidget system that you’re modifying here, and so we don’t want to make any new modifications to it right now. How about instead you refactor our new BarWidget class?”

- 举例：作为审阅者，可能你会说：”看起来做的不错，谢谢，但是，我们实际上是要在这个组件系统移除掉你修改的这些功能，所以我们不想现在在这个地方有任何的修改，考虑一下重构掉我们新的组件类吗？“

- Note that not only did the reviewer reject the current CL and provide an alternative suggestion, but they did it *courteously*. This kind of courtesy is important because we want to show that we respect each other as developers even when we disagree.

- 作为审阅者，拒绝当前变更并且给与一个折中的建议，这不失为一种礼貌的做法，我们虽然不认同当前修改，但是也要充分给与开发者应有的尊重。

- If you get more than a few CLs that represent changes you don’t want to make, you should consider re-working your team’s development process or the posted process for external contributors so that there is more communication before CLs are written. It’s better to tell people “no” before they’ve done a ton of work that now has to be thrown away or drastically re-written.

- 如果收到过多你不想审阅的变更，你应该考虑一下是不是团队开发流程或者外部贡献者发布的流程需要重新设计，使得在变更前取得更多的沟通。及时的说"不"可以减少团队的大量重写或者改进的工作量

  ## Step Two: Examine the main parts of the CL

  ## 步骤2：评估变更中的主要部分

- Find the file or files that are the “main” part of this CL. Often, there is one file that has the largest number of logical changes, and it’s the major piece of the CL. Look at these major parts first. This helps give context to all of the smaller parts of the CL, and generally accelerates doing the code review. If the CL is too large for you to figure out which parts are the major parts, ask the developer what you should look at first, or ask them to [split up the CL into multiple CLs](https://google.github.io/eng-practices/review/developer/small-cls.html).

- 找出单文件或者多文件中主要变更的部分。一个文件中通常会存在大量的逻辑修改，也是主要的代码块变更，这个主要的部分需要先评审，这会帮助你从更小部分的修改中得到上下文。同时也能加速代码评审的速度。如果变更内容过多评审人不能在里面找出主要部分，请询问开发者主要部分，然后要求开发者在[大变更中拆分出多个变更](https://google.github.io/eng-practices/review/developer/small-cls.html)降低颗粒度。

- If you see some major design problems with this part of the CL, you should send those comments immediately, even if you don’t have time to review the rest of the CL right now. In fact, reviewing the rest of the CL might be a waste of time, because if the design problems are significant enough, a lot of the other code under review is going to disappear and not matter anyway.
- 如果在变更中找出一些主要的设计问题，应该立刻将问题反馈给开发者，即使你没有足够的时间将剩下的审阅完成。实际上，将剩下的审阅评审完是浪费时间的行为。因为如果设计问题足够的重要，其他在评审下的代码都应该被优化或者是无关紧要的。
- There are two major reasons it’s so important to send these major design comments out immediately:
- 这里有两个主要的观点表明留下立即主要设计评论的重要性：
  - Developers often mail a CL and then immediately start new work based on that CL while they wait for review. If there are major design problems in the CL you’re reviewing, they’re also going to have to re-work their later CL. You want to catch them before they’ve done too much extra work on top of the problematic design.
  - 开发者通常会发一个邮件，然后在等待审阅期间根据变更立刻开始新的工作 ，如果你在审阅的时候变更中有几个主要的设计问题，开发者要在之后的变更中重新进行开发。你要想方设法在他们做了大量额外有设计问题之上的工作前喊停。
  - Major design changes take longer to do than small changes. Developers nearly all have deadlines; in order to make those deadlines and still have quality code in the codebase, the developer needs to start on any major re-work of the CL as soon as possible.
  - 主要设计变更通常比小修改耗费的时间更多。开发每项任务都有对应的截止时间，为了能赶上工期并且还能让代码保持一定的质量，开发者要尽可能快的开始任何的返工工作。

## Step Three: Look through the rest of the CL in an appropriate sequence

## 步骤3：按适当的顺序查看剩下的变更

- Once you’ve confirmed there are no major design problems with the CL as a whole, try to figure out a logical sequence to look through the files while also making sure you don’t miss reviewing any file. Usually after you’ve looked through the major files, it’s simplest to just go through each file in the order that the code review tool presents them to you. Sometimes it’s also helpful to read the tests first before you read the main code, because then you have an idea of what the change is supposed to be doing.
- 一旦为整个变更确认没有主要的设计问题后，试着搞清楚这些文件中的逻辑顺序，同时确保不要漏掉任何一个需要审阅的文件。通常看完几个主要文件后，最简单的方式是通过代码审查工具的提示去浏览每一个文件。有时读主要代码之前先看测试对阅读也十分有帮助，因为这样才知道哪些是应该做修改的。



## 下一篇：[代码审阅时效](https://github.com/Trojan0523/Code-Review-Docs/blob/main/Speed%20of%20Code%20Reviews.md)

