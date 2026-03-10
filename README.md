# IG Skills Hub

IG Skills Hub is an open skills marketplace that gives AI agents native access to financial markets. Search instruments, execute trades, track positions, monitor accounts, and manage watchlists, all through natural language.

Built by IG. Built for everyone.

We're not building this just for IG products. Skills Hub is designed for the entire trading ecosystem: any agent, any framework. Whether you're building on LangChain, CrewAI, or your own stack, your agents can plug into markets with a few lines of config.

## About This Repository

Each skill lives in its own folder and contains a `SKILL.md` file with YAML frontmatter and structured instructions.

Browse the existing skills to understand patterns and naming conventions before contributing.

| Skill | Description |
|-------|-------------|
| [ig/spot](skills/ig/spot/) | Execute trades and manage positions |
| [ig/market-data](skills/ig/market-data/) | Search markets, prices, and sentiment |
| [ig/account](skills/ig/account/) | View balances and transaction history |
| [ig/watchlist](skills/ig/watchlist/) | Create and manage watchlists |

## Contribution

We welcome contributions.

To add a new skill:

1. Fork the repository and create a new branch:
   ```
   git checkout -b feature/<skill-name>
   ```

2. Create a new folder containing a `SKILL.md` file.

3. Follow the required format:
   ```yaml
   ---
   name: <Skill Name>
   description: A clear description of what the skill does and when to use it.
   metadata:
     version: <Skill Version>
     author: <Your Github Username>
   license: MIT
   ---

   # <Skill Name>

   [Add instructions, examples, and guidelines here]
   ```

4. Open a Pull Request to main for review. Once approved, the skill will be merged.

## Disclaimer

IG Skills Hub is an informational tool only. IG Skills Hub and its outputs are provided to you on an "as is" and "as available" basis, without representation or warranty of any kind. It does not constitute investment, financial, trading or any other form of advice; represent a recommendation to buy, sell or hold any assets; guarantee the accuracy, timeliness or completeness of the data or analysis presented. Your use of IG Skills Hub and any information provided in connection with this feature is at your own risk, and you are solely responsible for evaluating the information provided and for all trading decisions made. IG does not endorse or guarantee any AI-generated information. Any AI-generated information or summary should not be solely relied on for decision making. AI-generated content may include or reflect information, views and opinions of third parties, and may also include errors, biases or outdated information. IG is not responsible for any losses or damages incurred as a result of your use of or reliance on the IG Skills Hub feature. IG may modify or discontinue the IG Skills Hub feature at its discretion, and functionality may vary by region or user profile. CFD and spread betting trading involves risk. The value of your investment may go down or up, and you may not get back the amount invested. You are solely responsible for your investment decisions and IG is not liable for any losses you may incur. Past performance is not a reliable predictor of future performance. You should only invest in products you are familiar with and where you understand the risks. You should carefully consider your investment experience, financial situation, investment objectives and risk tolerance and consult an independent financial adviser prior to making any investment. This material should not be construed as advice.
