[[Yuntao Bai]]∗ , [[Saurav Kadavath]], [[Sandipan Kundu]], [[Amanda Askell]], [[Jackson Kernion]]
[[Anthropic]]
https://ai-plans.com/file_storage/4f32fa39-3a01-46c7-878e-c92b7aa7165f_2212.08073v1.pdf

1. Big Pictures
	1. The authors of this research sought to find a method of scalable reinforcement learning that didn't require human feedback or input
	2. As Ai assistants become bigger and are able to access more information, using direct human labels will become an unreasonable task, so the ability for AI to govern itself will be of upmost importance. Especially as we near a point where AI could start to become to smart / efficient for us to improve it ourselves.
	3. Wanted to study the simple possibilities for using AI systems to help supervise other AIs
	4. Wanted to improve prior work training a harmless AI assistant by eliminating evasive response (i can't provide a response to this question / request)
2. Approach
	1. Ai is given a "constitution" - a short list of written rules or principles.
		1. Training process, AI answers tough / harmful questions
		2. AI critiques its own answers by asking "Did i break any principles" then revises or rewrites its answer to follow the constitution
		3. Then Ai compares two answers to a tough question and decides which one follows the constitution better
		4. AI feedback helps it learn to prefer responses that follow the rules
3. Evidence
	1. As model size increased and the use of CoT was introduced, AI systems became significantly better at identifying and reasoning about potentially harmful outputs.
	2. Applying model-generated critiques and subsequent revisions led to monotonic improvements in harmlessness metrics over several stages
	3. The paper reported that RL-CAI models trained with constitutional methods were preferred by crowdworkers and considered less harmful and less evasive 
	4. Limitations: Over-optimazation can lead to models producing responses that were generic, so while technically less harmful they weren't necessarily better responses
	5. asking crowdworkers to rate responses based on harmlessness / evasiveness as opposed to helpfulness skewed the way they rated responses 
	6. increasing the number of constitutional principles did not significantly improve harmlessness scores but did improve the diversity of responses. (Impact of this diversity of responses was not studied quantitatively)
	7. AI generated critiques were sometimes inaccurate or overstated raising the risk of removing content that was not actually harmful or missing subtler forms of harm.
	8. Progress was made on reducing harm using Constitutional AI, but their models still aren't fully resistant to sophisticated attacks or nuanced harms especially as models scale up. Robustness and scaling both need much more work
4. Personal Takeaway
	1. How can we make models more immune to red-teaming (no existing method that makes a model immune to such attempts)
	

  