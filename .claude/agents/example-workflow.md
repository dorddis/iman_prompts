# Twitter Post Generation System - Example Workflow

## How to Use the Podcast-to-Twitter Subagent System

### Prerequisites
1. Ensure all subagent files are in `.claude/agents/` directory
2. Have your podcast transcript ready (text file or markdown)
3. Have any existing brand guidelines or style preferences documented

## Step-by-Step Workflow

### Step 1: Prepare Your Transcript

Place your podcast transcript in the project directory. The transcript should ideally include:
- Speaker names
- Basic timestamps (if available)
- Episode metadata (title, date, guests)

Example structure:
```
Episode: The Future of AI
Guest: Dr. Jane Smith
Date: January 2025

Host: Welcome to the show...
Guest: Thanks for having me...
```

### Step 2: Invoke the Main Orchestrator

Use the Task tool to launch the podcast-twitter-orchestrator agent:

```
"Process this podcast transcript located at [transcript.txt] and generate a complete Twitter content package including standalone tweets, threads, and a posting schedule."
```

The orchestrator will automatically:
1. Process the transcript
2. Extract key content
3. Build tweets and threads
4. Quality check everything
5. Create a posting schedule

### Step 3: Review the Output

The system will generate:

```
output/
├── standalone-tweets.md     # 5-7 individual tweets
├── thread-sequences.md       # 2-3 complete threads
├── quote-highlights.md       # Key quotable moments
├── posting-schedule.md       # 7-day posting plan
├── qa-report.md             # Quality assurance results
└── visual-suggestions.md     # Recommended graphics
```

## Example Input and Output

### Sample Input (Podcast Excerpt)

```markdown
Host: What's the biggest mistake you see founders making?

Dr. Smith: The biggest mistake? They fall in love with their solution instead of the problem. I've seen brilliant engineers spend years perfecting a product nobody wants. The successful founders I know are obsessed with the problem, not their solution. They'll pivot ten times if that's what it takes to solve the real pain point.

Host: Can you give an example?

Dr. Smith: Sure. Last year, I worked with a startup that spent $2M building an AI platform for restaurants. Beautiful tech, cutting-edge algorithms. But they never talked to restaurant owners. Turns out, restaurants didn't need AI - they needed better scheduling software. The company pivoted, built a simple scheduling tool, and hit $1M ARR in 6 months.
```

### Sample Output

#### Standalone Tweets Generated:

**Tweet 1:**
```
"The biggest mistake? Founders fall in love with their solution instead of the problem"

- Dr. Jane Smith on why startups fail

The successful ones stay obsessed with the pain point, not their product 🎯
```

**Tweet 2:**
```
$2M burned on AI nobody wanted
6 months later: $1M ARR

The difference?
They finally talked to their customers

Sometimes the simple solution wins 📊
```

#### Thread Generated:

```
1/ A startup burned $2M building AI for restaurants

Then they discovered something that changed everything

Here's the pivot playbook that took them to $1M ARR in 6 months: 🧵

2/ The Beginning:
• Brilliant engineers
• Cutting-edge AI platform  
• Beautiful tech
• Zero customer interviews

Recipe for disaster 📉

3/ The Reality Check:

After burning through $2M, they finally asked restaurant owners what they needed

The answer wasn't AI
It wasn't complex
It was embarrassingly simple...

4/ The Truth:

Restaurants didn't need AI algorithms

They needed basic scheduling software

That's it.
That's the whole pain point.

5/ The Pivot:
- Killed the AI platform
- Built simple scheduling tool
- Launched in 30 days
- First customer in week 1

6/ The Results:
Month 1: $10K MRR
Month 3: $50K MRR  
Month 6: $85K MRR

$1M ARR achieved ✅

7/ The Lesson:

"Fall in love with the problem, not your solution"

Your tech doesn't matter if it doesn't solve real pain

Talk to customers BEFORE you build

8/ Ask yourself:
- Have I validated this with 20+ customers?
- Am I solving a problem or pushing a solution?
- Would I pay for this myself?

What problem are you actually solving?
```

#### Posting Schedule:

```markdown
# 7-Day Twitter Posting Schedule

## Day 1 (Monday)
- 9:00 AM: Hook Tweet (Tweet 1)
- 2:00 PM: Engagement question about founder mistakes

## Day 2 (Tuesday)  
- 10:00 AM: Full thread (8 parts, spaced 2 mins apart)
- 5:00 PM: Quote tweet thread with additional context

## Day 3 (Wednesday)
- 11:00 AM: Statistics tweet (Tweet 2)
- 3:00 PM: Follow-up poll about pivoting

## Day 4 (Thursday)
- 9:30 AM: Key quote graphic post
- 4:00 PM: Reply to high-engagement responses

## Day 5 (Friday)
- 10:00 AM: Recap best insights
- 2:00 PM: Share related resource

## Weekend
- Light engagement, respond to comments
- Prepare next week's content

## Metrics to Track:
- Impressions per tweet
- Thread completion rate
- Profile clicks
- Follow conversions
- Reply sentiment
```

## Advanced Usage

### Customizing Output

You can modify the orchestrator's instructions for specific needs:

**For more tweets:**
```
"Generate 10-15 standalone tweets focusing on actionable insights"
```

**For LinkedIn cross-posting:**
```
"Also create LinkedIn-optimized versions (longer format)"
```

**For specific topics:**
```
"Focus extraction on [leadership/growth/technical] content only"
```

### Working with Different Podcast Formats

**Interview Style:**
- System preserves Q&A dynamic
- Extracts both questions and answers
- Creates threads from conversation flow

**Solo Episodes:**  
- Focuses on key teachings
- Extracts frameworks and systems
- Builds educational threads

**Panel Discussions:**
- Captures different viewpoints
- Creates debate-style threads
- Highlights consensus/disagreement

## Troubleshooting

### Common Issues and Solutions

**Issue: Too few tweets generated**
- Solution: Ensure transcript is properly formatted with clear speaker labels
- Check that transcript has sufficient content (minimum 15 minutes recommended)

**Issue: Tweets exceed character limit**
- Solution: The QA agent should catch this, but manually verify critical tweets
- Use the twitter-qa-agent directly for fixes

**Issue: Brand voice mismatch**
- Solution: Create a brand-voice.yaml config file with specific guidelines
- Include example tweets that match desired voice

## Best Practices

1. **Always Review**: While the system is thorough, human review ensures quality
2. **Test Variations**: Use the A/B test suggestions to find what resonates
3. **Track Performance**: Monitor which content types perform best
4. **Iterate**: Refine the subagent prompts based on results
5. **Maintain Context**: Keep successful examples to train future iterations

## Next Steps

After successfully generating content:

1. **Visual Creation**: Use the visual suggestions to create graphics
2. **Scheduling**: Implement the posting schedule using Buffer/Hootsuite
3. **Monitoring**: Track engagement metrics
4. **Optimization**: Feed high-performing patterns back into the system
5. **Scaling**: Process multiple episodes in batch for content calendar

---

This system transforms hours of manual content creation into an efficient, quality-controlled process that maintains your brand voice while maximizing engagement potential.