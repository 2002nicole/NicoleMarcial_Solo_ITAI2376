# REFLECTION.md
## What worked well in your implementation. What did not work and how you handled it. 
Thankfully this project went very smoothly because I did my best to keep it focuesed on cookie recipe adaptation instead of trying to build a general baking assistant.
The strongest part of my implementation was that the agent used several different components instead of only relying on the language model. 
Most of the issues came from testin real prompts and noticing small problems in the output. One example, was when I tested a recipe by changing the batch size and the sugar amount
was shown in tablespoons instead of converted into a cleanr cup measurement. I had to adjust the code and fromatting so ingredietn amounts were presented more clearly.

## The biggest technical challenge and how you solved it. 
I think for me one of the biggest technical challenges was building and debugging the Gradio App. 
It wasn't technically required for this assignment but I wanted to have a good user-friendly interface for the demo.
Since this was my first time using Gradio, it was a bit difficult and confusing fixing chat formats, example prompts, layout, and colors that didn't look right. 

## If you switched from Single Agent to Multi Agent or vice versa, explain why.
I did not switch my original decision (single agent) because it fit my project better and matched my current skil level. My goal was to build one focused assistant
that could understand a cookie related request, use tools, retrieve helpful baking context, and return an adapted recipe or guidance.
If I were to do a multi-agent I would probably overcomplicate stuff and I would have a harder time debugging. Staying with a single agent helped me build something more realistic and stable.

## What you would build next if you had another semester.
I think if I were to build another agent, I would expand this idea into a more advanced baking assistant for cakes and frostings,. 
There's a lot of things that comes with baking cakes (compared to cookies) such as pan size, baking time, layer heights, fillings, frosting/buttercream tyoe, servings, flavor pairings, and decoration goals..
Because of that, a cake-focused agent could be very useful for beginner bakers.
If I had to impove the cookie agent, I would do so by adding stronger recipe memory, more precise unit conversion, and a larger baking knowledge base. I would also want the agent to remember previous user preferences
so it could give more personalized suggestions. 

