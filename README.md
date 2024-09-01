# Overview
LLMProxy serves as a guardrail, like a firewall between your application and an AI provider, to stop certain types of generative AI risks like some found in the [AI incident database](https://incidentdatabase.ai/). 

The implementation compares inputs and outputs to policies (using sentence embeddings) at Cloudflare, to enforce customizable input and output policies. 
Using guardrails such as these may help accelerate your deployments' adherence to security and compliance expectations of your choice, such as reducing risky content or queries.

# Key Features
- Customizable Policies: Define and configure input/output policies to match your security needs.
- Cosine Similarity Enforcement: Use configurable thresholds to measure the similarity between message embeddings and predefined policies.
- Blocking and Reporting: Automatically block and report any violations detected during input or output inspections.
- Seamless Integration: Acts as a middleware, forwarding approved requests to the AI provider.

# Configuration / usage
- Similarity Threshold (sim_thresh): Adjust this value to set the sensitivity of policy enforcement.
- Input/Output Policies: Modify the policies object to define the patterns or instructions that the proxy should detect and block. Thanks to embeddings, these are not keywords but notions, so it's better to include a diversity of issues to prevent rather than synonyms.
- Deploy LLMProxy in your own cloudflare worker or preferred hosting provider to add an additional layer of control and security over your applications' LLM traffic.
- All incoming requests and outgoing responses will be inspected based on the cosine similarity of their embeddings against the defined policies.

For more information on generative AI risks, see [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/) and [MIT's AI Risk taxonomy](https://airisk.mit.edu/)

## Example
Below is an example of the proxy's workflow:
- Input Inspection: Incoming requests are checked against configured input policies. If a violation is detected based on the cosine similarity of embeddings, the request is blocked.
- Output Inspection: Responses from the AI provider are similarly inspected. Violations in the output lead to blocking the response from reaching the application.

## Limitations
LLMProxy is not a silver bullet but a proof of concept. Read more about [LLM risks and the state of guardrails](https://arxiv.org/pdf/2406.12934)

# Notes
- For further background on the concept and motivation, see this [blog](https://emiledelcourt.com/llmproxy)
- This project is licensed under the MIT License.

