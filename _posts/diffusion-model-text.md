




The way we generate language is not quire word by work, or toekn by token. Rather we first come up with the basic idea of what we are looking to express, and then we express it, the best we can using words. This first stage sugests that maybe a diffusion model is appropriate for language modeling tasks after all. Here are some crude thoughts on DDPMs applied to text: 

- Represent a chunk of text (say, a paragraph) as a BERT embedding. This is the true (noise-free) sequence represeting this chunk. 
- Now, we prgressively add noise to the embedding vectors repreesnting each token. This makes progressively noisy copies of the original data point. 
- We learn to reverse the process. Unlike images, each data point would have different lengths, because the length of each BERT sequence can be different. 
- Next, we learn to do autoregressive modeling a tthe abstract thought level. And then we do autoregressive modeling at the token level. The long context for each is different. The token level autoregressive modeling doesn't require a very long context window in terms of number of tokens. 
