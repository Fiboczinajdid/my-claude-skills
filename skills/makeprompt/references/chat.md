# Prompts for a one-off chat

Pasted once at the start of a claude.ai conversation and read once.

- Put supplied material (text, data, code) in XML tags near the top and the task after it; with long material, a question placed at the end is answered better.
- If the task depends on an attachment, say in the prompt that the material is attached and remind the user to attach it.
- If the task needs current information or a specific website, ask Claude to search or browse it, to say how much it actually covered, and to name what it could not reach instead of filling gaps from memory.
- For "is this possible" questions, ask for a direct answer first, then the options with their trade-offs, then concrete steps for the recommended one.
- State the output shape: length, structure (prose, list, table), language.

By detail level:
- Concise: the question or task in a few sentences.
- Standard: + context, output shape, what to do when something can't be checked.
- Full: + criteria for judging options, edge cases, an example of the expected output if one exists.
