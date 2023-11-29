
## VannaHooks: AI Infrastructure for Uniswap V4

<u>Short Description</u>: Building on-chain AI inference infrastructure for the Arbitrum Ecosystem + creating AI-driven Uniswap V4 hooks to reduce AMM impermanent loss.

<u>Category</u>: Uniswap on Arbitrum Ecosystem + Open Contribution

<u>Requested Funding</u>: $240,000 ARB

<u>Core Team</u>:

<b>Matthew Wang</b>

- Background: Computer Engineering at Northwestern University

- Experience: Building AI inference on decentralized infrastructure at Vanna Labs + research engineering in options market-making at Two Sigma.

- Focus: Project Supervisor + Vanna Infrastructure

<b>Manav Aggarwal</b> 

- Background: Computer Science at Stanford University

- Experience: Protocol/infrastructure engineering at Celestia + data infrastructure engineering at Two Sigma.

- Focus: Vanna Infrastructure + Arbitrum Integration

<b>Tony Lee</b> 

- Background: Computer Science at Northwestern University

- Experience: Quantitative research in crypto market-making at Ava Labs + quantitative options trader at Susquehanna International Group (SIG).

- Focus: Uniswap LVR Modeling 

<b>Andrew Wang</b> 

- Background: Applied Mathematics at UT Austin

- Experience: Machine learning research at Capital One + machine learning engineering at Oracle.

- Focus: Uniswap LVR Modeling

<b>Jeffrey Lin</b> 

- Background: Finance at National Taiwan University

- Experience: Experience building blockchain infrastructure, smart contract development, web3 security auditing, has also won 10+ web3 awards through multiple hackathon projects like ZKAlpha.

- Focus: Uniswap Hook Smart Contracts

  
<b><u>Project Context</b></u>:

Before diving into our project proposal, articles and concepts to help establish familiarity with relevant subjects:
* [Impermanent Loss — Half of Uniswap V3 Users Lose Money](https://hackernoon.com/half-of-uniswap-v3-users-lose-money-heres-why)
* [LVR — Quantifying the Cost of Providing Liquidity](https://a16zcrypto.com/posts/article/lvr-quantifying-the-cost-of-providing-liquidity-to-automated-market-makers/)
* Vanna Labs: [How on-chain ML models can reduce impermanent loss](https://medium.com/vanna-labs/protecting-amm-liquidity-with-on-chain-machine-learning-5aa1af546528)
* [Uniswap V4 Vision](https://blog.uniswap.org/uniswap-v4#hooks-custom-pools): Call for V4 hooks like Dynamic Fees
* Vanna Labs: [Applications of AI/ML on the Blockchain](https://medium.com/vanna-labs/applications-ai-ml-on-the-blockchain-dc4ef449179e)
* [Introduction to zkML](https://blog.spectral.finance/the-state-of-zero-knowledge-machine-learning-zkml/)


## Project Overview

The Vanna Labs team is developing blockchain infrastructure to run AI/ML inference trustlessly and natively on-chain. 

Our goals for UAGP are four-fold:
1. Integrate Vanna’s trustless AI/ML inference features into an Arbitrum Orbit chain to bring the power of inference to the Arbitrum ecosystem. 
	- We want to make it super easy for developers on Arbitrum to develop intelligent applications that use AI models directly from their smart contracts powered by Vanna. 
2. Research and integrate AI models that quote dynamic fees into Uniswap V4 hooks to provably reduce impermanent loss for liquidity providers on Uniswap (Arbitrum).
3. Provide a sandbox ecosystem to allow developers to research and develop their own AI/ML-driven hooks for Uniswap V4.
4. Drive research and exploration for using AI/ML intelligent compute to benefit Uniswap (in addition to dynamic fees), this may include:
	- Using market regime models (like Hidden Markov Models) to vary fees in different market environments
	- Building AI/ML models to measure average toxicity of users’ trades as a way to vary fees using a Uniswap hook.
	- Exploring collaboration with Spectral Finance to incorporate AI-generated credit scores to reduce fees with a Uniswap hook.
	- Creating ONNX models for pricing derivatives of tokens on Uniswap.

## Vanna Information

<i>Vanna Labs is building blockchain infrastructure to support trustless native AI/ML inference directly computed, secured, and verified on-chain; all designed in a way that is so seamless that leveraging AI/ML in dApps is as easy as a simple function call.</i>

<b><u>Vanna Blockchain</b></u>:

We currently have experimented with a blockchain testnet (currently used internally for testing and experimentation):
- RPC Endpoint: [http://dev-rpc.vannalabs.ai:9545](http://dev-rpc.vannalabs.ai:9545)
- Explorer url: [http://dev-rpc.vannalabs.ai:4000](http://dev-rpc.vannalabs.ai:4000)
- ChainID: 901
- Faucet: [https://vanna-faucet.vercel.app/](https://vanna-faucet.vercel.app/)

Vanna is building an Arbitrum Orbit Chain and bring the power of trustless AI and ML inference to the Arbitrum ecosystem, and we’re super excited to start with tackling use-cases we’ve already researched for Uniswap’s AMMs.

Vanna is a blockchain network that settles on Arbitrum, and will be able to utilize cross-chain messages to communicate with Uniswap on Arbitrum via ArbOS precompiles. The ArbOS precompiles are able to thus, expose the inference results compute on Vanna to the Uniswap contracts on Ethereum to adjust the fees dynamically within the AMM pools.

<Architecture Diagram>
![Architecture Diagram](https://raw.githubusercontent.com/VannaLabs/Vanna-UAGP-Proposal/main/VannaTXFlow.jpg)
	
[Here is a demo of our testnet running an on-chain fee calculation model.](https://drive.google.com/file/d/1cRb3HNAH88VSRqKRlgwKyNJvdmB3Uaj5/view?usp=sharing)

<b><u>Vanna's AMM Experimentation</b></u>:

In quant finance, market-makers typically increase the spreads and widen their quotes during periods of elevated volatility or risk. This makes sense because market makers want to be compensated more for taking on more risk.

However, this mechanism doesn’t really exist in DeFi AMMs yet, but one can imagine a similar mechanism through dynamically adjusting fees for AMM pools depending on the market regime. Uniswap put “[dynamic fees based on volatility](https://blog.uniswap.org/uniswap-v4)” as a key feature they’d like to see implemented via hooks in Uniswap V4.

But why are dynamic fees important? Dynamic fees are important because in periods of high volatility, impermanent loss risk is elevated and opportunistic traders are able to profit by arbitraging the pool and rebalancing the ratio of the assets in the pool; by dynamically increasing fees charged by the AMM pool during these periods of elevated risk, we are able to deter arbitrage activity and/or compensate liquidity providers more (with higher fees) for taking on high-risk order flow. Arbitrageurs are a net harm to an AMM because when they profit, it incurs impermanent loss on the liquidity providers of the AMM pool.  

![](https://miro.medium.com/v2/resize:fit:720/format:webp/1*GZgFveapPG23BGUrOCW5Nw.jpeg)

Needless to say, impermanent loss is one of the biggest pain-points of AMMs. [A16z Research introduced the idea of exploitable LVR](https://a16zcrypto.com/posts/article/lvr-quantifying-the-cost-of-providing-liquidity-to-automated-market-makers/), suggesting a new metric for benchmarking the “performance” of an AMM by quantifying the amount of net profit the AMM exposes to opportunistic arbitrageurs. There is also [published research](https://arxiv.org/abs/2111.09192?ref=hackernoon.com) that shows that for [more than half of Uniswap V3 liquidity providers](https://hackernoon.com/half-of-uniswap-v3-users-lose-money-heres-why), they lose more money via impermanent loss than they profit from fees.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*auvql7rBAWRski5z.png)

Vanna enables native (on-chain) and trustless (zkML-secured) AI/ML inference, so we want to work with Uniswap to create a V4 hook on Arbitrum that uses price volatility to feed into an ML model on Vanna to trustlessly compute dynamic fees for Uniswap AMM pools. 

We’ve already built a sample proof-of-concept regression model that we have running on the Vanna testnet that computes dynamic spreads; <i>however</i>, there is still a significant amount of room for improvement. In order to develop an effective model, we need to undergo significantly more thorough research, testing, and iterative model development; and we have planned to do as such as part of UAGP.

For the experiment model, we obtained orderbook data from the Kraken exchange and trained the model to quote like centralized market-makers. The model regresses different windows of price volatility on the top-of-the-book spread quoted by market-makers on Kraken. In other words, it uses moving-window volatility to predict spreads.

We then ran a simulation and modeled traders as purely opportunistic, in order to benchmark the performance of our spread calculation model. Note that the simulation time period is quite short, and only meant for demonstration purposes, we plan to create a more robust simulation platform as part of UAGP. The green line represents the ETH-USDT price while the red represents the volatility, which is the rolling standard deviation of the price.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*S58TUXZGuoZlkto0bgrS7w.png)

As one can see from the results below, in this simulation, we are able to see the difference in liquidity provider balance increase over time (red: difference between dynamic fee model vs static fee model), especially when the exploitable LVR opportunity (represented as blue bars) was high. Empirically one can observe the dynamic fees protect user liquidity through charging higher fees to arbitrageurs during periods of elevated volatility.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*cltuyKc3OmiBXZ84F0j_jg.png)

The key lies in reducing the net instantaneous exploitable LVR during periods of high volatility by increasing fees

The experiment was part of a hackathon project the Vanna team had worked on, [codebase linked here](https://github.com/jeff0723/VannaSwap). 

## Arbitrum Ecosystem Impact 

<i>Vanna aims to bring trustless AI/ML to the Arbitrum ecosystem by building an Arbitrum Orbit Chain that can run inference. This would allow for developers within the Arbitrum ecosystem to use Vanna’s infrastructure to leverage sophisticated models in a way that is trustless, secure, and scalable to build sophisticated dApps that are more intelligent.</i>


![Vanna's AI use-cases](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*KQNIQ5ZZIs2trWyyvg1v_A.png)

<b><u>Nerd-sniping for Arbitrum</b></u>:

Vanna opens entirely new verticals for nerd-sniping more engineers and researchers into the Arbitrum ecosystem to develop applications on Arbitrum with Vanna’s infrastructure as an orbit chain. Here I highlight multiple new areas of development that Vanna creates for the collective and can get engineers and researchers alike excited!

1. Quantitative Research in DeFi 
	- With secure on-chain inference, we can leverage machine learning to enable sophisticated features within DeFi! Opens the door to quantitative research talent from quant funds like Two Sigma, Jane Street, Citadel…etc.
	- Quant Research talent can help build DeFi risk-engines, AMM spread calculation models, quantitative trading models for vaults, price forecasting models, crypto derivative pricing models…etc that all live on-chain.
2. AI Research
	- Attracts researchers who are interested in building AI/ML models and researching the use of AI models in a Web3 context. New AI models could enable interesting use-cases like autonomous agents on-chain.
	- Interesting Web3 x AI/ML specific research areas like decentralized federated learning or fully homomorphic encryption (for model privacy)!
3. zkML R&D
	- Attract developers and researchers who are interested in applied zkML, as Vanna is one of the first blockchain networks to enshrine zkML cryptography into the blockchain architecture.
4. AI Application Developers
	- Attracts blockchain developers who are excited by being able to develop new applications empowered by AI/ML. Like dynamic NFT art generation projects, use-specific language generation protocols, Web3 chatbots or agents…etc.

![DefAI Meme](https://miro.medium.com/v2/resize:fit:828/format:webp/0*WhuzuE-LJxwi0o7t.jpg)

## Uniswap Ecosystem Impact

<i>Vanna plans to use machine learning models secured by zkML to intelligently compute dynamic fees for Uniswap pools using V4 hooks to reduce net impermanent loss for liquidity providers (LPs). We also plan to explore various other use-cases of intelligent compute and how Vanna can be used to further improve the Uniswap user experience.</i>

![AMM Dynamic Fees](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*tPMzEZHd0fPaiKkyjp4_XQ.png)

From the simulation experiment we conducted above, we are able to see that there is a quantifiable benefit to dynamically varying fees for AMM pools by using a model to emulate how centralized market-makers quote on orderbook exchanges.

This model can prove to be extremely powerful for an AMM like Uniswap:
- <b>Liquidity Providers win</b> because they will suffer from less impermanent loss in the long run.
- <b>Regular traders win</b> because when folks trade normally most of the time they can actually benefit from lower fees.
- <b>Opportunistic arbitrageurs lose</b> because they make less net profit (due to higher fees) when they arb a pool. 

We wrote more about our experiment here, [this article](https://medium.com/vanna-labs/protecting-amm-liquidity-with-on-chain-machine-learning-5aa1af546528) contains high-level comments about our implementation and thoughts.

<b><u>Vanna x Uniswap Synergies</b></u>:

We want to create a positive sum game for Vanna x Uniswap, here are some benefits that we think Uniswap will benefit from for this partnership.

1. <b>Improving Uniswap (less LP impermanent loss)</b>
	- The most obvious benefit for Uniswap is that Vanna’s models can help improve the liquidity provision experience for LPs on Uniswap, by reducing the impermanent loss they suffer from via dynamic fees.
2. <b>Opening doors to AI on Uniswap</b>
	- The Vanna x Uniswap integration opens the doors to new quant research and ML engineering talent that may be interested in building sophisticated models to help improve the initial fee calculation model, or build out other sophisticated models to help build more features or solve other problems on Uniswap. Examples:
		- Systematic trading strategies 
		- AI-driven smart execution
		- Models to predict trade toxicity for varying trading fees
		- Using HMM market regime models to vary fees in different market environments
		- Incorporate AI-generated credit scores to vary fees
		- Creating models for pricing derivatives of tokens on Uniswap.

3. <b>Opening doors to new applications on Uniswap</b>
	- Kickstarting the Vanna x Uniswap integration will encourage more intelligent dApps to be developed on Uniswap in the future. AI driven vaults that use Uniswap for trading, ML driven risk management that uses Uniswap to de-risk or hedge portfolio exposure, ETFs that have smart rebalancing…etc.
4. <b>Tech-forward PR</b>
	- With AI and ML being increasingly popular and ubiquitous, having a progressive approach to integrating these technologies to improve the experience of users reflects well on the protocol team. It’s good to be a trailblazer in piloting new technology, demonstrating a forward-thinking culture.


## Vanna's Planning

<b><u>KPIs</b></u>:

1. <b>AI/ML x Web3 Adoption</b>: Achieve 3000+ inference transactions a month after Sepolia Testnet launch.
2. <b>Reduced Impermanent Loss in Uniswap pools</b>: Benchmark AMM performance with new Uniswap hooks that empirically demonstrate lower impermanent loss for liquidity providers.
3. <b>Community Growth</b>: Grow community of AI x Web3 enthusiasts to 10K users and/or developers. Notably, we’d like to get the community excited about AI/ML use-cases with Uniswap V4 Hooks.
4. <b>Partnerships</b>: Form strategic partnerships to collaborate with 2-3 other projects interested in building AI/ML dApps in Arbitrum or Uniswap with Vanna.


<b><u>Milestones</b></u>:
1. <b>Orbit Chain Development</b> (Months 1-3): Develop blockchain with AI/ML inference features available on-chain, exposed via precompile.
	- Deliverable: Working blockchain testnet with secure on-chain AI/ML inference enabled in addition to being able to expose inference cross-chain with Arbitrum and other dApps on Arbitrum. 
	- Budget: 50K
2. <b>Data Cleaning, Data Exploration, and Model Research</b> (Months 1-2): Acquire clean market data for key asset pairs and begin data exploration around spread calculation model development.
	- Deliverable: N/A
	- Budget: 20K
3. <b>Simulation Platform and Model Development</b> (Months 2-4): Develop AMM trading simulation platform, and start iterative testing and development on different models.
	- Deliverable: Comprehensive research article about the developed ML model and benchmark simulations in liquidity provision against popular AMM models like CPMM and CSMM.
	- Budget: 35K
4. <b>Uniswap Contract Development </b>(Months 3-4): Develop and deploy Uniswap V4 Contracts with the AI/ML enabled dynamic fee hooks
	- Deliverable: Working Uniswap V4 hooks using AI/ML-enabled dynamic fee hooks + Uniswap V4 deployment on Vanna. 
	- Budget: 35K
5. <b> Engineering Productionalization</b> (Months 5-6): Productionalization and deployment of the Vanna Network with robust hardware (like GPU inference nodes) along with all the relevant contracts and integrations. Seek security audit services to do a final security audit pass on our infrastructure and contracts.
	- Deliverable: Production-ready blockchain network on the Sepolia Testnet deployed with block explorer and docs, supporting reasonable amounts of inference transaction throughput with production hardware.
	- Budget: 65K
6. <b> Marketing, Technical Writing, and Community Development</b> (Months 3-6): Author technical whitepaper with tech specs, write technical documentation, and conduct social media marketing for awareness.
	- Deliverables: Technical whitepaper, tweets, medium articles, and technical documentation.
	- Budget: 35K

For important milestones, we'll be authoring and publishing articles and thought pieces that outline our research, experience, and learnings as well.

<b><u>Conclusion</b></u>:

Conclusively, we think on top of being tech-forward in researching and experimenting with more intelligent compute in a quantitative DeFi context, the Vanna <> UAGP project can bring about numerous benefits to the Uniswap and Arbitrum ecosystems alike. 

For Arbitrum, we’d like to unlock doors to new tools, technology, and paradigms of programming that can enable developers to build AI-empowered dApps and features. 

For Uniswap, we’d like to improve the user experience through intelligent features that can lead to protected user liquidity, more efficiency, and an increased frictionless experience; but more importantly, we’d like to create the tooling necessary for developers and researchers to continue iterating on use-cases of AI with Vanna for Uniswap’s AMMs.

<b><u>Vanna Labs Links</b></u>:
* [Vanna Testnet Demo](https://drive.google.com/file/d/1cRb3HNAH88VSRqKRlgwKyNJvdmB3Uaj5/view?usp=sharing)
* [Vanna Labs Twitter](https://twitter.com/0xVannaLabs)
* [Vanna Labs Github](https://github.com/orgs/VannaLabs/repositories)
* Vanna Labs Article: [The State of Blockchain x AI Inference](https://medium.com/vanna-labs/the-state-of-blockchain-x-ai-inference-c0e386356d49) 
* Vanna Labs Article: [How on-chain ML models can reduce impermanent loss](https://medium.com/vanna-labs/protecting-amm-liquidity-with-on-chain-machine-learning-5aa1af546528)
* Vanna Labs Article: [Applications of AI/ML on the Blockchain](https://medium.com/vanna-labs/applications-ai-ml-on-the-blockchain-dc4ef449179e) 


