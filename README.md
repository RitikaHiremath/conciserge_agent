# Martin The Concierge : Your Personalised Path to Adventure.

Planning a trip is time-consuming and overwhelming, forcing travellers to sort through endless information before ever enjoying their vacation. Now Martin's got you covered! Enjoy effortless customised travel literary based on your preference. Our concierge-based AI agent, Martin eliminates this hassle by delivering personalised, preference-driven travel recommendations, helping users spend less time planning and more time experiencing their journey.

## The Problem :

Planning is more exhausting that the trip itself!

- Information Overload: Having a million tabs open from from travel blogs to You tube vlogs, trying to find the perfect place for your vacation.
- Context switching: jumping from maps to weather forecasts to comparing the rates of flights and hotel bookings from various websites.
- The Reality Gap: Is the restaurant even open on that day? Do I need to make a reservation in advance?

## Solution:

This is where Martin, swoops in as a saviour. Simply tell Martin your destination and preferences and he will do everything for you.

Recommendation: Curates personalized suggestion on where to go and what to do perfectly tailored to users unique preferences.
Information: Provides factual answers to user queries about planning, destination, opening hours, weather etc eliminating the need to switch between multiple websites and apps.
Booking: Secures the best deals for flight, hotels and appointments by making the bookings directly for user.
Architecture:

Martin is multi-agent AI system built with Google's ADK and it follows a hierarchical approach.
It consists of:

- A router agent that classifies user intent into one of the three categories (specialist agents)
- A Distributor that acts as the orchestrator and based on the output from the router, it routes the query to the appropriate agent by invoking via AgentTool .
- A workers agent that consists of the three specialist agents:Booking Agent, Information agent, Recommendation Agent that run concurrently to ensure good responsiveness.
- The Router, Distributor and Workers are connected sequentially.

`User Query -> [Router -> Distributor->Workers(booking|| info||recommendation)]-> Martin response `
 
## Tools:

Martin uses two key functions `make_booking` and `get_location_context` wrapped as ADK FunctionTool in order to simulate booking confirmations and location data retrieval. This enables LLM to invoke them as needed.
get_location_context is designed to interface with a real MCP server, allowing Martin to access booking platforms, weather updates, maps and more without manual API integration. However currently it is returning static data.
The Google Search tool is also wrapped as built in FunctionTool and equips both Information and Recommendation agent. The Distributor agent also used this `google_search` as a fallback when necessary.
Martin uses Runner integrated with InMemorySessionServices to ensure context retention making multiturn conversation flow naturally without forgetting important details.
The run_concierge_session function overlooks the full session lifecycle. It handles creating/resuming sessions to maintain continuity and ensures user queries are processed in order enabling dynamic, interactive conversations.

## Value statement:

Using Martin_the_concierge reduces the planning time by 90% reducing my analysis fatigue. Now I don't spend hours anxiously researching for hidden gems or the most trendiest spots. Martin does it all. All I have to worry about are my outfits !! Martin has me covered from personalized recommendation , real time lookups and booking coordination .
In future, it would be possible to integrate MCP serves directly to enable actual end to end bookings , making the experience even more effortless.

## Conclusion:

Martin is a shift from static search method to a dynamic, intelligent travel planning. By coordinating specialized agents martin delivers complete personalized solutions and not just random information. It transforms the stressful flow of planning into a seamless conversational experience. Martin makes planning as exciting as the journey.
