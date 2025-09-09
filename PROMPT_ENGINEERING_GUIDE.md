# Prompt Engineering Best Practices Guide (August 2025)

## Core Principles

### 1. Clarity and Specificity Above All Else
- **Be explicit about what you want**: Clear structure and context matter more than clever wording
- **Include specific details**: Audience, tone, format, length, and constraints
- **Avoid ambiguous language**: Each instruction should have only one interpretation
- **Specify output format**: Tell the model exactly how you want the response structured

### 2. Use Structured Prompting
- **Break prompts into clear sections** using delimiters or tags
- **Order matters**: Test different content arrangements:
  - Option 1: [examples] [context] [input]
  - Option 2: [input] [examples] [context]  
  - Option 3: [examples] [input] [context]
- **Use consistent formatting**: Maintain uniform structure across all examples

### 3. Leverage Model-Specific Features

#### For Claude (Anthropic):
- **Use XML tags extensively**: Claude was trained with XML tags
  - `<instructions>`, `<context>`, `<examples>`, `<answer>`, `<thinking>`
- **Place key instructions in human messages** rather than system messages
- **Prefill responses**: Start the assistant's response to guide format
- **Be explicit and direct**: Claude 4 models excel at precise instruction following

#### For GPT (OpenAI):
- **Use markdown formatting** for structure
- **System messages are powerful**: Use them for role-setting and high-level context
- **Temperature control**: Set to 0 for factual tasks, higher for creative tasks
- **Use the latest models**: Newer models are easier to prompt engineer

#### For Gemini (Google):
- **Leverage multimodal capabilities**: Can process text, images, video, audio
- **Break complex tasks into sub-prompts**: Gemini handles sequential tasks well
- **Use structured prompts feature** in Google AI Studio for few-shot learning
- **Include fallback instructions**: Tell the model what to do when uncertain

## Essential Prompt Components

### 1. Task Definition
```
Role/Persona: "You are a [specific expert role]..."
Task: "Your task is to [specific action verb]..."
Goal: "The objective is to [desired outcome]..."
```

### 2. Context Provision
- **Background information**: Provide all necessary context
- **Constraints**: Specify limitations (word count, style, format)
- **Target audience**: Describe who will consume the output
- **Domain-specific information**: Define technical terms or acronyms

### 3. Output Specifications
- **Format requirements**: Lists, paragraphs, JSON, markdown, etc.
- **Length constraints**: Word count, character limit, or number of points
- **Style guidelines**: Tone, formality level, technical depth
- **Structure template**: Provide exact format example when needed

## Advanced Techniques

### 1. Chain-of-Thought (CoT) Prompting
```
"Think through this step-by-step:
1. First, identify...
2. Then, analyze...
3. Finally, conclude...
Show your reasoning before providing the final answer."
```

### 2. Few-Shot Learning
- **Provide 3-5 diverse examples** showing desired input-output templates
- **Quality over quantity**: One excellent example beats ten mediocre ones
- **Consistent formatting**: All examples must follow the same structure
- **Cover edge cases**: Include examples of tricky scenarios

### 3. Self-Consistency
- **Generate multiple reasoning paths** for complex problems
- **Compare outputs** to identify the most consistent answer
- **Use for critical decisions** where accuracy is paramount

### 4. Meta-Prompting
- **Create prompts that generate prompts**: Useful for template creation
- **Focus on logical structure** rather than specific content
- **Maintain abstraction** while being clear about requirements

## Prompt Engineering Workflow

### 1. Planning Phase
- Define success criteria clearly
- Identify required information and context
- Choose appropriate prompting technique
- Select the right model for the task

### 2. Development Phase
```
1. Start with a basic prompt
2. Test with 5-10 diverse inputs
3. Identify failure templates
4. Refine one element at a time
5. Re-test after each change
```

### 3. Optimization Phase
- **Measure key metrics**: Accuracy, relevance, format compliance
- **A/B test variations**: Compare different prompt structures
- **Document what works**: Save successful templates with version tags
- **Iterate based on data**: Use feedback to continuously improve

## Common Pitfalls to Avoid

### 1. Over-Prompting
- **Don't over-constrain**: Too many rules can confuse the model
- **Avoid contradictions**: Ensure all instructions align
- **Skip redundancy**: Don't repeat the same instruction in different ways

### 2. Under-Specifying
- **Don't assume context**: Provide all necessary information
- **Avoid vague terms**: Replace "good" with specific criteria
- **Define edge cases**: Specify behavior for unusual inputs

### 3. Poor Example Selection
- **Don't use inconsistent examples**: All must follow the same template
- **Avoid biased samples**: Include diverse, representative cases
- **Don't overfit to examples**: Too many can make responses rigid

## Model-Agnostic Best Practices

### 1. Iterative Refinement
- **Start simple, add complexity gradually**
- **Test each change systematically**
- **Keep a prompt changelog**
- **Measure performance objectively**

### 2. Error Handling
```
"If you're unsure about any aspect, respond with 'I need clarification on [specific aspect]'"
"If the input is invalid, explain why and suggest a correction"
```

### 3. Safety and Boundaries
- **Include ethical guidelines** when appropriate
- **Specify content restrictions** clearly
- **Add fallback behaviors** for edge cases
- **Test with adversarial inputs**

## Prompt Templates

### Basic Task Template
```
Role: You are a [role/expertise].
Task: [Specific action to perform]
Context: [Background information]
Requirements:
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]
Input: [User's specific input]
Output Format: [Desired format]
```

### Analysis Template
```
Analyze the following [type of content]:
<content>
[Insert content here]
</content>

Consider these aspects:
1. [Aspect 1]
2. [Aspect 2]
3. [Aspect 3]

Provide your analysis in the following structure:
- Summary (2-3 sentences)
- Key findings (bullet points)
- Recommendations (numbered list)
```

### Creative Generation Template
```
Generate a [type of content] with these characteristics:
- Tone: [specific tone]
- Length: [word/character count]
- Audience: [target audience]
- Key themes: [list themes]
- Must include: [specific elements]
- Must avoid: [elements to exclude]

Begin with [specific opening] and end with [specific closing].
```

## JSON Parsing Rules for Python .format() Compatibility

When creating prompts that include JSON examples and will be processed with Python's `.format()` method, follow these critical formatting rules:

### 1. Double Brace Escaping
- **Always use `{{` and `}}` instead of `{` and `}`** in JSON examples
- This prevents Python's `.format()` from interpreting braces as format placeholders
- Single braces will cause KeyError exceptions when the prompt is formatted

### 2. Correct JSON Example Format
```
CORRECT (for .format() compatibility):
{{
  "topic_title": "The specific insight or concept title",
  "content_summary": "Detailed explanation of the insight",
  "relevance_score": 3
}}

INCORRECT (will break with .format()):
{
  "topic_title": "The specific insight or concept title", 
  "content_summary": "Detailed explanation of the insight",
  "relevance_score": 3
}
```

### 3. Template Variable Distinction
- Use single braces `{variable_name}` for actual template variables that should be replaced
- Use double braces `{{` `}}` for literal JSON structure in examples
- This allows proper variable substitution while preserving JSON syntax

### 4. Complete Example
```
<output_format>
Return ONLY a JSON array with extracted topics for {target_audience}:
[
  {{
    "topic_title": "The insight title here",
    "content_summary": "Explanation for {brand_archetype} voice",
    "score": 4
  }}
]
</output_format>
```

### 5. Validation Checklist for JSON in Prompts
- [ ] All JSON examples use double braces `{{` `}}`
- [ ] Template variables use single braces `{variable}`
- [ ] No mixed single/double brace usage in JSON
- [ ] Examples will parse correctly after `.format()` processing

## Quick Reference Checklist

Before finalizing any prompt, verify:
- [ ] Clear, unambiguous instructions
- [ ] All necessary context provided
- [ ] Output format explicitly specified
- [ ] Examples included (if helpful)
- [ ] Edge cases addressed
- [ ] Tested with diverse inputs
- [ ] Performance metrics defined
- [ ] Version documented

## Key Metrics for Evaluation

1. **Accuracy**: Does the output match expectations?
2. **Consistency**: Are similar inputs producing similar outputs?
3. **Completeness**: Is all requested information included?
4. **Format Compliance**: Does output match specified structure?
5. **Relevance**: Is the content on-topic and useful?
6. **Efficiency**: Token usage vs. output quality ratio

## Final Tips

1. **Less is sometimes more**: Start with minimal instructions and add only as needed
2. **Test edge cases early**: Identify breaking points before production
3. **Version control prompts**: Track changes like code
4. **Share successful templates**: Build a team knowledge base
5. **Stay model-agnostic when possible**: Design prompts that work across models
6. **Measure everything**: Data-driven iteration beats intuition
7. **Expect evolution**: Models improve; revisit prompts periodically

---

*Remember: Prompt engineering is both art and science. These guidelines provide a foundation, but experimentation and iteration based on your specific use case will yield the best results.*