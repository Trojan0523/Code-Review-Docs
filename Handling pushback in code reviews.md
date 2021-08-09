# Handling pushback in code reviews

# 处理代码审阅的阻力

- Sometimes a developer will push back on a code review. Either they will disagree with your suggestion or they will complain that you are being too strict in general.
- 有时开发者会打回代码审阅，要么就是他们不同意你的建议，要么就是他们会抱怨审阅者对代码的过于严格。

## Who is right?

## 谁是对的

- When a developer disagrees with your suggestion, first take a moment to consider if they are correct. Often, they are closer to the code than you are, and so they might really have a better insight about certain aspects of it. Does their argument make sense? Does it make sense from a code health perspective? If so, let them know that they are right and let the issue drop.
- 当开发者不同意你的建议的时候，花点时间去考虑他们的述词是否正确。通常，他们会比你更了解自己写的代码，所以他们有可能真的对于某些方面会有一个更好的洞察力，他们的争论是否有意义？对于代码质量的看法是否有意义？如果是这样的话，认同他们的观点，关掉问题。
- However, developers are not always right. In this case the reviewer should further explain why they believe that their suggestion is correct. A good explanation demonstrates both an understanding of the developer’s reply, and additional information about why the change is being requested.
- 然而，开发者也不总是对的。某种情况下，审阅者应该进一步解释为什么审阅者坚信他们的建议是正确的。一个好的解释既表明了对开发者回复的理解，又能解释清楚为什么请求的变更需要格外的信息做支撑。
- In particular, when the reviewer believes their suggestion will improve code health, they should continue to advocate for the change, if they believe the resulting code quality improvement justifies the additional work requested. **Improving code health tends to happen in small steps.**
- 特别要指出的是， 审阅者坚信他们的建议会改善代码质量的时候，如果他们坚信带来的额外工作请求能带来代码质量的提升，他们应该继续提倡修改。代码质量的改善需要通过不断的修改完成。
- Sometimes it takes a few rounds of explaining a suggestion before it really sinks in. Just make sure to always stay [polite](https://google.github.io/eng-practices/review/reviewer/comments.html#courtesy) and let the developer know that you *hear* what they’re saying, you just don’t *agree*.
- 有时修改变更的真正落地需要经历几轮建议的解释，确保解释的过程中保持[礼貌](https://google.github.io/eng-practices/review/reviewer/comments.html#courtesy)，让开发者认识到你在倾听他们所说的事情。不要一味否定。

## Upsetting Developers

## 开发者的沮丧

- Reviewers sometimes believe that the developer will be upset if the reviewer insists on an improvement. Sometimes developers do become upset, but it is usually brief and they become very thankful later that you helped them improve the quality of their code. Usually, if you are [polite](https://google.github.io/eng-practices/review/reviewer/comments.html#courtesy) in your comments, developers actually don’t become upset at all, and the worry is just in the reviewer’s mind. Upsets are usually more about [the way comments are written](https://google.github.io/eng-practices/review/reviewer/comments.html#courtesy) than about the reviewer’s insistence on code quality
- 审阅者有时需要理解，如果坚持自己的改进建议，开发者会不会感到沮丧。有时候开发者的确会产生这样的感受，不过持续的时间很短，并且以后他们会对你帮助了他们进行代码质量改进心存感激。通常礼貌的评论并不会让开发者感到不适，这种不安只会在审阅者心中。不安更多的是在[编写评论的方式](https://google.github.io/eng-practices/review/reviewer/comments.html#courtesy)上而不是审阅者对于代码质量的坚持对于开发者造成的不安。

## Cleaning It Up Later

## 整理的拖延

- A common source of push back is that developers (understandably) want to get things done. They don’t want to go through another round of review just to get this CL in. So they say they will clean something up in a later CL, and thus you should LGTM *this* CL now. Some developers are very good about this, and will immediately write a follow-up CL that fixes the issue. However, experience shows that as more time passes after a developer writes the original CL, the less likely this clean up is to happen. In fact, usually unless the developer does the clean up *immediately* after the present CL, it never happens. This isn’t because developers are irresponsible, but because they have a lot of work to do and the cleanup gets lost or forgotten in the press of other work. Thus, it is usually best to insist that the developer clean up their CL *now*, before the code is in the codebase and “done.” Letting people “clean things up later” is a common way for codebases to degenerate.
- 一个常见的打回原因是因为开发者想把手上的活干完。他们不想为了这个变更审阅放下手上的活。所以他们会选择将手上的活干完，然后再去给代码做评审合并。有些开发者深知这种情况，会立刻写一个稍后待办列表去解决这个问题。然而经验告诉我们更多是开发者在写下原始变更，对清理这些变更情况会更少。实际上，他们如果不在现有变更后立即清理掉手上的活，他们永远不会去做这些事。并不是因为他们不负责任，而是他们手上有一大堆的活等着去做，工作的压力让他们忘记了去做修复。所以，应该坚持让开发者在代码入库前立即对提出的变更建议进行修复，让开发者知道这是一个降低代码质量比较普遍的方式。
- If a CL introduces new complexity, it must be cleaned up before submission unless it is an [emergency](https://google.github.io/eng-practices/review/emergencies.html). If the CL exposes surrounding problems and they can’t be addressed right now, the developer should file a bug for the cleanup and assign it to themselves so that it doesn’t get lost. They can optionally also write a TODO comment in the code that references the filed bug.
- 如果变更中出现新的复杂度较高的东西，除非是紧急的修改，不然要在提交前就要整理完毕。如果变更充斥着不少问题，而且目前解决不了，开发者需要将其整理为bug待修复列表，然后将任务分配给自己，以免丢失。他们还可以选择性在代码中写入待办bug修复的注释。

## General Complaints About Strictness

## 对于审阅严格的抱怨

- If you previously had fairly lax code reviews and you switch to having strict reviews, some developers will complain very loudly. Improving the [speed](https://google.github.io/eng-practices/review/reviewer/speed.html) of your code reviews usually causes these complaints to fade away.
- 如果审阅者以前的审核比较宽松，突然转向了较为严格的审阅方式，有些开发者可能会怨声较大，提高代码审阅速度可能会让这些抱怨声消退不少。
- Sometimes it can take months for these complaints to fade away, but eventually developers tend to see the value of strict code reviews as they see what great code they help generate. Sometimes the loudest protesters even become your strongest supporters once something happens that causes them to really see the value you’re adding by being strict.
- 有时候这些抱怨可能在几个月之后才能消退，但是最终开发者是愿意看到严格代码审阅下的价值，同时也能看到审阅者审阅下迭代的优秀代码。有时候吵的最凶的反而会成为你最大的拥趸，因为他们真正的看到严格下带来的额外价值。

## Resolving Conflicts

## 解决冲突

- 如果上述的情况还是解决不了你和开发者之间的矛盾，请遵循[代码审阅标准](https://github.com/Trojan0523/Code-Review-Docs/blob/main/eng-practices%20(%E5%B7%A5%E7%A8%8B%E5%B8%88%E5%AE%9E%E8%B7%B5).md)，这些准则可以帮助你去解决矛盾。

