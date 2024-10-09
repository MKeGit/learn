GitHub Copilot code completion features live directly within your IDE, where you write and review your code. GitHub Copilot integrates seamlessly with editors like Visual Studio Code or JetBrains, offering features such as autosuggestions, a multiple suggestions pane, and support for various coding styles. You primarily interact with GitHub Copilot through these IDE tools, and understanding how and where to use them helps you optimize its powerful code generation abilities.

In this unit, we cover:

- GitHub Copilot supported languages 
- Auto suggestions
- Multiple suggestions pane
- Support for different coding styles in suggestions
- How GitHub Copilot incorporates coding comments for suggestions


## GitHub Copilot supported languages
GitHub Copilot provides robust support for a wide range of programming languages and frameworks, with strong capabilities in:

- Python
- JavaScript
- TypeScript
- Ruby
- Go
- C#
- C++

While these languages receive exceptional support, GitHub Copilot can assist with many other languages and frameworks as well.


## Auto suggestions
Copilot offers code suggestions as you type: sometimes completing the current line, sometimes suggesting a whole new block of code. You can accept all, part, or ignore the suggestion. This ability to provide real-time, context-aware suggestions saves valuable development time by reducing the need to search for syntax, troubleshoot logic, or repeatedly write common patterns.

:::image type="content" source="../media/auto-completion-ghost-text.png" alt-text="Screenshot of auto completion ghost text.":::


## Multiple suggestions pane
When you're working on a code block and GitHub Copilot offers a suggestion, you see a grayed-out code snippet. To explore more options, hover over the suggestion to reveal the GitHub Copilot control panel.

:::image type="content" source="../media/multiple-suggestion-auto-completion-ghost-text.png" alt-text="Screenshot of multiple suggestion auto completion ghost text.":::

Click the forward or backward arrow buttons in the control panel to see the next or previous suggestions. You can also use keyboard shortcuts:
  - macOS: Option (⌥) or Alt+] (next), Option (⌥) or Alt+[ (previous) 
  - Windows or Linux: Alt+] (next), Alt+[ (previous)

:::image type="content" source="../media/suggestions-pane.gif" alt-text="Screenrecord of suggestions pane.":::

While GitHub Copilot is superb at suggesting code for you, it also demonstrates its ability to adapt through the following ways:

1. **Method Implementation**: When you start typing a method name, Copilot can suggest the entire implementation, following your established coding style.
2. **Naming Conventions**: It picks up on your preferred naming conventions for variables, functions, and classes.
3. **Formatting**: Copilot adapts to your indentation style, bracket placement, and other formatting preferences.
4. **Comment Style**: It can mimic your comment style, whether you prefer inline comments, block comments, or doc strings.
5. **Design Patterns**: When your project consistently uses certain design patterns, Copilot suggests code that aligns with these patterns.


## Using coding comments for suggestions
A key aspect of this capability is how it incorporates coding comments to enhance its suggestions. This section explores the various ways GitHub Copilot utilizes comments to improve its code completion and generation capabilities.

### Understanding Comment Context
When integrated into your existing codebase, GitHub Copilot uses various aspects of your code to provide more relevant suggestions, including code comments. Developers often use comments to clarify code intent and enhance collaboration, and Copilot, as your AI coding assistant, makes use of these comments in much the same way. By understanding the intent behind the comments, Copilot can provide more accurate and context-aware code suggestions through two key processes: 

1. **Natural Language Processing**: Copilot uses advanced natural language processing (NLP) techniques to interpret the meaning and intent behind comments in the code.
2. **Contextual Analysis**: It analyzes comments in relation to the surrounding code, understanding their relevance and purpose within the broader context of the file or project.


## Types of Comments Utilized
Copilot can work with various types of comments to inform its suggestions:
1. **Inline Comments**: Short explanations next to specific lines of code.
2. **Block Comments**: Longer explanations that might describe a function or class.
3. **Docstrings**: Formal documentation strings in languages like Python.
4. **TODO Comments**: Notes about future implementations or improvements.
5. **API Documentation**: Comments that describe the usage and parameters of functions or methods.


## Comment-Driven Code Generation
Copilot uses comments in several ways to generate and suggest code:
1. **Function Implementation**: When a function is described in comments, Copilot can suggest an entire implementation based on that description.

   :::image type="content" source="../media/multiple-line-code-completion-ghost-text.png" alt-text="Screenshot of multiple line code completion ghost text.":::

2. **Code Completion**: Copilot uses comments to provide more accurate code completions, understanding the developer's intent.

   :::image type="content" source="../media/whole-function--auto-completion-ghost-text.png" alt-text="Screenshot of whole function  auto completion ghost text.":::

   In this example, we have a comment describing a function to reverse a string. Based on this comment, Copilot is likely to suggest an implementation using Python's slice notation with a step of -1, which efficiently reverses the string.

3. **Variable Naming**: Comments can influence Copilot's suggestions for variable names, making them more descriptive and context-appropriate.

   :::image type="content" source="../media/variable-name-auto-completion-ghost-text.png" alt-text="Screenshot of variable name auto completion ghost text.":::

   Here, we have a comment describing a list of the user's favorite books. Copilot would likely suggest descriptive variable names that match the context. In this case, it suggested "favorite_books" as the variable name, which clearly describes the content of the list.

4. **Algorithm Selection**: When comments describe a specific algorithm or approach, Copilot can suggest code that aligns with that method.

   :::image type="content" source="../media/algorithm-auto-completion-ghost-text.png" alt-text="Screenshot of algorithm auto completion ghost text.":::

   In the example above, we provide comments that outline the steps of the bubble sort algorithm. Based on these comments, Copilot would likely suggest an implementation that closely follows the steps described.
