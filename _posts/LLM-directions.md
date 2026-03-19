Research directions with LLMs: 

- Separate out factual information from language learning: simple next token based training does not distinguish between these two. For example, the cross entropy loss for each of the missing tokens for the following two examples is the same: (a) I'm tired, so I'm going to rest for a ----. (b) the capital of France is -----. But the first example is geared towards learning language while the second is gewared toward learning factual knowledge. I think we should not really attempt to cram factual knowledge into a language model, beacause there is no limit to the amount of technical factual information we can keep adding to it, thereby bloating the # of parameters in the model. Many facts are time-sensitive. For example, the response to the question 'Who is the president of the of the USA?' should depend on when it is asked, not on when the model was trained. More importantly, we do not want a model to 'hallucinate' incorrect facts. 'Hallucinating' launguage artifacts is fine. One idea is to use a crude LLM to figure out which pieces of training data pertain to laungage and which pertain to facts, and then apply training loss only on non-factual tokens, or weight them differently. 

- Diffusion based generation (already happening in major labs) instead of autoregressive

- Slow thinking mode that accesses memory

- Ability to know when to be factual, and to check factualness

