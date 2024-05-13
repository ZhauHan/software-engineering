---
aliases: 
tags:
  - SoftwareEngineering
---
## Model View Controller Model

>[!note] Models
>* Models represent knwledge
>* Could be a single object, or some structure of objects
>* There should be one-to-one correspondence between the model and its functions on one hand and the represented world as perceived by the owner of the model.

>[!note] View
>* A visual representation of its model. It would ordinarily highlight certain attributes of the model and suppress others. It is thus acting as a presentation filter.
>* A view is attached to its model (or model part) and gets the data necessary for the presentation from the model by asking questions. It may also update the model by sending appropriate messages. All these questions and messages have to be in the terminology of the model, the view will therefore have to know the semantics of the attributes of the model it represents.
>

>[!note] Controllers
>* Link between a user and the system.
>* It provides the user with input by arranging for relevant views to present themselves in appropriate places on the screen.
>* It provides means for user output by presenting the user with menus or other means of giving commands and data.
>* The controller receives such user output, translates it into the appropriate messages and pass these messages on to one or more of the views.

> [!example] Example Website as an MVC
> ![[Pasted image 20240128230859.png]]
> 1. Model
> 	- The HTML is the "skeleton" of bedrock content. Text that communicates information to the reader.
> 2. View
> 	- The CSS adds visual style to the content. It is the "skin" that we use to flesh out our skeleton and give it a particular look. We can swap in different skins via CSS without altering the original content in any way. They are relatively, but not completely, independent.
> 3. Controller
> 	- The browser is responsible for combining and rendering the CSS and HTML into a set of final, manipulatible pixels on the screen. It gathers input from the user and marshals it to any JavaScript code necessary for the page to function. But here, too, we have flexibility: we can plug in a different brower and get comparable results. Some browsers might render it faster, or with more fidelity, or with more bells and whistles.
> 


