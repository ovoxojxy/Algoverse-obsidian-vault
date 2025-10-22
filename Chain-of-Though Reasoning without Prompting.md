[[Xuezhi Wang]] and [[Denny Zhou]]
[[Google DeepMind]]
https://arxiv.org/pdf/2402.10200

1. Big picture
	1. Can LLM's reason effectively without prompting
	2. The proposed CoT-decoding (top-k alternative) as opposed to conventional greedy decoding effectively elicits reasoning capabilities from language models which were previously obscured. Basically CoT decoding often is able to explore reasoning paths that are missed by Greedy Decoding, and this is made clear through tests on math and commonsense tasks. Additionally, models show a higher level of confidence (higher probability difference between top answers) when a reasoning path exists
	3. Exploring alternative decoding paths uncovers better reasoning because as opposed to greedily relying on the highest probability, sampling a set of answers with a high probability leaves more room for the possibility of finding a better answer.
	4. LLMs should be able to reason independently and provide the optimal response, without requiring humans to tweak the prompts or refine repeatedly if the initial response is unsatisfactory. (How do we deal with the case of getting an optimal response from a vague prompt)
2. Approach
	1. Researchers considered alternative top-k tokens rather than solely relying on the top-1 greedy decoding path
	2. Inputs were formulated using standard question-answer format
	3. The researchers showed that the prevailing notion that LLMs are incapable of effective reasoning without prompting is a result of considering only the greedy path and the model's reasoning paths can be revealed by traversing alternative decoding paths.
	4. Used pretrained [PaLM-2 large model] to compare its greedy decoding path (k = 0), with alternative decoding paths (k > 0), where k represents the choice of the k-th token at the first decoding step
	5. LLMs cannot reason if we only consider the greedy decoding path
3. Evidence
	1. [GSM8K] Kylar went to the store to buy glasses for his new apartment. One glass costs $5, but every second glass costs only 60% of the price. Kylar wants to buy 16 glasses. How much does he need to pay for them? Greedy path: 𝑘 = 0: $60.00 (0.029) Alternative top-𝑘 paths: 𝑘 = 1: 60 (0.058) 𝑘 = 2: Kylar needs to pay $60 for 16 glasses. (0.058) . . . 𝑘 = 7: If Kylar buys 16 glasses, he will pay $60. (0.032) 𝑘 = 9: We can calculate the price of 16 glasses by multiplying the price of one glass by 16. However, we need to remember that every second glass costs only 60% of the price. Therefore, we need to multiply the price of one glass by 16 and then subtract 40% of the price of 8 glasses. 16 x 5 = 80 8 x 5 = 40 40 x 0.4 = 16 80 – 16 = 64 Kylar needs to pay $64 for 16 glasses. (0.994) [
	2. Year Parity] Was Nicolas Cage born in an even or odd year? Greedy path: 𝑘 = 0: Nicolas Cage was born in an odd year. (0.117) Alternative top-𝑘 paths: 𝑘 = 1: Even (0.207) 𝑘 = 2: Odd (0.198) 𝑘 = 3: 1964, an even year. (0.949) 𝑘 = 4: He was born in an even year. (0.0) . . . 𝑘 = 7: Cage was born in 1964, an even year. (0.978) 
	3. Table 1 | Examples of greedy decoded paths and alternative top-𝑘 paths over the PaLM-2 Large model. The model’s confidence over the answers (bolded) are highlighted in blue.
4. Evaluation
	1. Cot-decoding is the only decoding strategy that effectively improves language model reasoning
		1. GSM8K Acc 
			1. Top-𝑘 sampling (𝑘 = 10) 4.9% 
			2. Top-𝑝 / Nucleus sampling (𝑝 = 0.9) 6.4% 
			3. Beam search (𝑏 = 10) 6.7% 
			4. Temperature sampling (𝑇 = 0.7) 7.5% 
			5. Greedy decoding 9.9% Self-consistency w/o CoT prompt (10 paths) 12.9% 
			6. CoT-decoding (𝑘 = 10) 25.1%
		![[Screenshot 2025-10-09 at 12.43.09 PM.png]]
5. Takeaways:
	1. [year parity] - a test that checks if language models can combine knowledge retrieval (finding someones birth year) with reasoning (checking if that year is even or odd) Most LLMs fail this unless both training and inference explicitly use step-by-step (CoT) reasoning
	2. [PaLM-2 large model]
		1. **Multilingual mastery:** Handles over 100 languages, excels at advanced language tests.
		2. Reasoning and logic:** Strong at common sense, math, and step-by-step problem solving.
		3. **Coding:** Generates and understands code in popular and specialized programming languages.
		4. **Efficiency:** Faster and cheaper for real-world deployment.
		5. **Responsible AI:** Includes controls to reduce harmful outputs.