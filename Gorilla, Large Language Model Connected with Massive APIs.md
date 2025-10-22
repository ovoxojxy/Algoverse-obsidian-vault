Authors [[Fanijia Yan]],[[Huanzhi Mao]], [[Charlie Cheng-Jie Ji]], [[Ion Stoica]], [[Joseph E. Gonzalez]], [[Tianjun Zhang]], [[Shishir G. Patil]]
Source: https://gorilla.cs.berkeley.edu/blogs/8_berkeley_function_calling_leaderboard.html

1. Big picture
	1. Leaderboard covers How accurately and robustly different LLMs perform function calling, including complex, multi-step, and parallel calls, in practical real-world software scenarios
	2. Function tool calling is becoming core to the next generation of AI-powered applications where LLMs must interact directly with software tools services and APIs on behalf of users not just answer questions in text
	3. Leaderboard highlights current strengths and limitations of LLMs in this key area, helps model developers focus on practical issues, and provides enterprises with guidance on choosing and deploying models for automation
	4. Identifies common model failures and provides actionable data for further research and fine-tuning, making it an important resource for the entire AI/ML community interested in true agentic AI and safe, reliable tool-using language models.
2. Approach
	1. Benchmark uses a large, diverse dataset of 2000 question function answer pairs spanning multiple programming languages and application domains
	2. dataset entries consist of realistic user questions structures function documentation and ground-truth answers internally sourced and generated from various website and practical scenarios
	3. Evaluation categories:
		1. Simple function: Single function, single call
		2. multiple function: Multiple functions provided, model selects the correct one 
		3. parallel function: Model triggers multiple calls in parallel
		4. parallel multiple function language and scenario specific test for REST, SQL, Java And Javascript
		5. Function relevance detection: Model must withhold calling if no suitable function exists
	4. Evaluation Metrics:
		1. Abstract Syntax Tree Evaluation: Parses model output function calls and checks strict correctness of function names, parameter presence types value matches and order very robust for code based tasks
		2. Executable Evaluation: Model output is executed and checked for correct result, structure and live API response consistency
		3. Cost and Latency: Measures model inference speed and computes estimated financial cost per 1000 function calls for each model
		4. All-or-Nothing Evaluation: For multi-output tests, every required function call must be correct for the answer to count
3. Evidence
	1. Simple Function Calling:
		1. Both GPT-4 and Claude and fine tuned open-source models, OpenFunctions-v2 & Gorilla, perform well in simple strighforward function calling tasks. For these scenarios, open-source solutions can be as effective as commercial ones
	2. Complex/Advanced function calling
		1. Proprietary models (GPT-4 and Claude) shw superiority for handling multiple, parallel, and complex chained function calls. Open source models lag significantly once tasks require the model to plan, select among several options or invoke functions in parallel
	3. Function Relevance Detection:
		1. Detecting when no function whould be called is challenging for all models. Some models, especailly chat optimized ones, hallucinate function calls even when none are suitable
	4. Domain and Language Robsutness:
		1. Models perform best in data-abundant,common programming domains(Python, Rest), but performance drops in niche areas like finance, law, or domain-specific APIs Handling of extended types(Java HashMap, javascript objects) is spotty
	5. Real-world executability
		1. There are notable gaps between correctly formatted fucntion calls and fucntion calls that actually exectue succesfully. Many output calls are "correct" by structure but fail in practice due to missing mandatory details, parameter type errors or omitted URLs for API calls
	6. Strengths:
		1. Strong in simple, Direct API use,Open source models with dedicated finetuning are closing the gap for basic use cases reducing dependence on proprietary APIS
	7. Limitations:
		1. Models struggle with parameters that need conversion (percentages into decimals)
		2. Hallucination
		3. All current open-source and most proprietary models struggle with multi-step function chaining, planning, and coordinated parallel calls-key capabilities for truly agentic AI systems
		4. Coverage and correctness drop off in non-mainstream functions (sports, law, finance), indicating the need for more domain-adapted models and data
4. Personal Takeaways
	1. More research is needed in safe function calling