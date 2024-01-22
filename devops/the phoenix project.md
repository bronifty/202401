“The Phoenix Project” is a novel about DevOps whose takeaways describe global and local maxima in flow & resource efficiency. Resource efficiency is micromanagement while flow efficiency is making sure everything gets done.

The global maxima (flow state aka getting things done) is a lean production technique whereas the local maxima (maxxing out resource task hours) is a bottleneck.

Busybody bottleneck management techniques have a proper engineering rationale for why they are wrong and also costly and inefficient as well as ineffective.

In complex systems, error states are expected and work should be managed so problems in design and operations are revealed. These bug fixes result in new organizational knowledge. The tactical approach to enabling these revelations is by creating fast or tight feedback and feedforward loops with small work batches and incremental improvements. Definitions: - feedback: unit, integration, end-to-end test results in lower envs, telemetry logs and observability in production - feedforward: Capacity planning, risk assessments, predictive analysis, and pre-deployment testing

Note: this is an outer loop discussion so feedback refers to the outer loop (ci/cd) as opposed to the inner loop (dev). Dev's tight feedback loop is HMR etc

The strategic approach to enabling an environment of discovery and continuous improvement (a learning organization) is cultural. The ideal technology culture is a high trust one reinforcing life long learning and risk taking with a scientific approach to process improvement and product development. Dr. Ron Westrum identified 3 types of management cultures: 1. Pathological: characterized by large amounts of fear and threat; people often hoard info, withhold it for political reasons, or distort it to make themselves look better; failure is often hidden 2. Bureaucratic: characterized by rules and processes, often to help individual departments maintain their turf; failure is processed through a system of judgment, resulting in either punishment or mercy 3. Generative: characterized by actively seeking and sharing info to enable the org to better enable its mission; responsibilities are shared throughout the value stream; failure results in reflection and genuine inquiry











- complex systems often have a high degree of interconnectedness of tightly coupled components and system-level behavior often cannot be explained merely by the behavior of individual components 
- complex systems do not necessarily have the characteristic of idempotency (doing the same thing multiple times gives the same result), leading to the conclusion that static checklists and "best practices" are insufficient to provide a holistic representation of the system
- failure states should be expected and accommodations made for individuals experiencing error conditions such that an environment is created fostering growth and learning (autopsies made without blame) to transform failure into feedback that enables growth
	- talk about the 3 types of cultures generative bureaucratic and p-something the one that is negative 

- a safe env is created when 4 conditions are met:
	1. complex work is managed so problems in design and operations are revealed
	2. problems are swarmed and solved resulting in construction of new knowledge
	3. local knowledge is transferred across the org
	4. leaders create other leaders 

- see problems as they occur (telemetry aka logs & observability aka centralization + automation of logs collection and monitoring)
	- feedback loops are a critical part of a learning org and systems thinking
	- fast feedback and feed-forward loops include automated build with unit and integration test with deploy

orgs with problems rigidly defined work and stonewalled suggestions for improvement, with a culture of fear and low trust where failure is punished
orgs with success dynamically defined work 

high trust culture reinforcing life long learning and risk taking with a scientific approach to process improvement and product development 


In complex systems, error states are expected and work should be managed so problems in design and operations are revealed. These bug fixes result in new organizational knowledge. The tactical approach to enabling these revelations is by creating fast or tight feedback and feedforward loops with small work batches and incremental improvements.

Definitions:
- feedback: unit, integration, end-to-end test results in lower envs, telemetry logs and observability in production
- feedforward: Capacity planning, risk assessments, predictive analysis, and pre-deployment testing

The strategic approach to enabling an environment of discovery and continuous improvement (a learning organization) is cultural. The ideal technology culture is a high trust one reinforcing life long learning and risk taking with a scientific approach to process improvement and product development. 

Dr. Ron Westrum identified 3 types of management cultures: 
1. Pathological: characterized by large amounts of fear and threat; people often hoard info, withhold it for political reasons, or distort it to make themselves look better; failure is often hidden
2. Bureaucratic: characterized by rules and processes, often to help individual departments maintain their turf; failure is processed through a system of judgment, resulting in either punishment or mercy
3. Generative: characterized by actively seeking and sharing info to enable the org to better enable its mission; responsibilities are shared throughout the value stream; failure results in reflection and genuine inquiry 