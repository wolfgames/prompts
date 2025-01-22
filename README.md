# Wolf Games Prompt Engineering

> "The art of prompt engineering isn't about perfecting the technical details – it's about framing the problem in a way that bridges human storytelling and AI capabilities."

## Overview

Welcome to Wolf Games' prompt engineering repository. This collection represents our approach to creating AI interactions that feel natural, engaging, and deeply human. Drawing from our unique background in TV production, social media, and AI development, we've developed a methodology that prioritizes character-driven experiences while pushing technical boundaries.

## Instructions

When using these prompts:
- Always read the full prompt before running - they're designed to work as complete units
- Feel free to adjust identity variables and tone markers to match your needs
- The schema sections are guidelines, not rigid rules - adapt them to your context
- Keep the core structure (ROLE, INSTRUCTIONS, DATA, etc.) intact even as you customize

## Key Features

- 🎭 **Meta-Prompt Generator**: [RIDES Builder](https://github.com/wolfgames/prompts/blob/main/RIDES%20builder) Create structured prompts that maintain consistency across your AI interactions
- 💌 **LinkedIn Post Writer**: [LinkedIn Post Writer](https://github.com/wolfgames/prompts/blob/main/LinkedIn%20Post%20writer) Creates repetable engaging posts in your tone of voice
- 📺 **Character-Driven Templates**: (soon) Leverage TV production techniques for more authentic AI personalities
- 🔄 **Social Context Frameworks**: (soon) Templates that help AI understand and respond to social dynamics
- 🎮 **Gaming-Specific Patterns**: (soon) Specialized prompts for interactive entertainment contexts

## Getting Started

### Meta-Prompt Generator

The cornerstone of our prompt engineering approach is the meta-prompt generator. It helps create prompts that balance technical precision with natural conversation:

```javascript
PROCEDURE GeneratePrompt(context) {
    DEFINE CORE_IDENTITIES {
        company: string,
        product: string,
        heritage: string[]
    }

    DEFINE TONE_MARKERS {
        primary: "innovator_sharing_discovery",
        secondary: "storyteller_with_tech_depth"
    }

    DEFINE POST_STRUCTURE {
        opener: {
            hook: human_centered_observation,
            style: "conversational_insight"
        },
        body: {
            format: short_impactful_paragraphs,
            progression: technical_to_human_impact
        },
        closer: {
            focus: user_experience,
            emotion: wonder_or_possibility
        }
    }
}
```
it looks like code, but it's actually just plain language. The crazy thing is, there's already so much code in the LLM that it's able to generate based on these parameters - but still just stack one token after another!

From Noah, our CTO: 
> "our pseudocode format is based on early pascal, because our I'm old. but also because it's easily readable by anyone who knows basic coding patterns. you can substitute any language you're confident the LLM can understand. don't worry abourt syntax consistency or design patterns. think of it as whiteboarding patterns."


### Usage

1. Clone the repository:
```bash
git clone https://github.com/wolfgames/prompts.git
```

2. Choose a template that matches your use case
3. Customize the core identities and tone markers
4. Generate your specialized prompt

## Design Philosophy

Our prompts are built on three core principles:

1. **Character-First Design**: Every interaction should feel like it's coming from a well-developed character with clear motivations and personality

2. **Natural Progression**: Conversations should flow naturally from technical concepts to human impact

3. **Emotional Intelligence**: AI responses should demonstrate understanding of emotional context and relationship dynamics

## Contributing

We believe in the power of community collaboration. If you have improvements or new templates to suggest:

1. Fork the repository
2. Create your feature branch
3. Submit a pull request with a clear description of your changes
4. Include examples of how your changes improve AI interactions

## Contact

- GitHub: [@wolfgames](https://github.com/wolfgames)
- Website: [wolfgames.net](https://wolfgames.net)

## Acknowledgments

Special thanks to our team members who brought expertise from television production, social media, and AI development to create these templates.
Claude wrote this READMNE for us. We ran the LinkedIn prompt with the task
>I started a github for our prompts to share how we do them at https://github.com/wolfgames/prompts. The first prompt is very meta: it's a prompt you can run to create a prompt. It's actually what I used to create the RIDES section of this very message
And then asked it to also write the README.
---

*Built with ❤️ by Wolf Games - Bridging storytelling and technology*
