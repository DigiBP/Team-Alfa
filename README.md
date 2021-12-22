# Team-Alfa

***
Authors:   
Lendrit Malushi,
Sandro Heimann,
Basil Knobel,
Sandro Eugster
*** 

## List assumptions:

- Clients come in and directly go to the screen
- To start the consultancy the customer has to slide his &quot;Krankenkassenkarte&quot; into the screen
- Clients choose whether they want self service or not
- There is always someone ready to support the people using the screen and is a pharmacist
- The screens scanners can read handwritten prescription notes from doctors
- Non-Prescription drugs are stored behind the screen and drop out
- Prescription drugs need to be checked by the Pharmacist
- Drugs in the drug dispenser are always stored and readily available


## Introduction

The team set out to work on the group project number six &quot;Digital pharmacy&quot; and created the fictitious pharmacy called &quot;Happy pharma&quot;. At this point, we would like to give again a special thanks to the FHNW lecturers from the module digitalisation of business processes who supported us with valuable advice during the project phase.

Happy pharma continuously strives to offer its customer the best service as possible. As part of its strategic assessment and outcome, Happy pharma decided to streamline its core process &quot;customer orders drugs&quot;. Thereby, state of the art technology was deployed, and customer feedback was considered to respect the important concept of customer centricity. From a technical perspective, the open-source workflow engine camunda was utilized following BPMN 2.0 methodology. Finally, services such as chatbots, google forms and excel sheets were integrated.

## As is process

The as is process &quot;order drugs&quot; from Happy pharma consists to a great extent of personnel intensive tasks. Except for the warehouse system, there are no digital activities included. The pharmacists still assist in simple customer drug requests having potentially less time for customers with a complex issue.

![sone kack bild vom as is prozess](images/asis.png?raw=true "Title")

## Assumptions

As this is a hypothetical case, several assumptions were made to facilitate such a automation. Some of the assumptions are of technical nature, other assumptions are rather of a general environment basis. These assumptions are made as a way to demonstrate the case later on.

Firstly it is assumed when the clients enter the pharmacy the self-service screen is readily available and ready to use. The clients that enter directly go to the screen and enter their health insurance card to facilitate payment at the end of the process. As soon as the card is entered the process starts which is described in detail in the following chapter To-Be Process.

If clients choose to go with the personal assistance over the self-service, there is always a pharmacy assistant or pharmacist ready to help them out. The scanners that are implemented in the self-service screen are able to pick up handwriting and validate the data and recognize whether e prescription is valid or not.

As a security measure, the self-service machine only is able to dispose non-prescription based drugs. The prescription drugs need to be handed out by qualified personnel, therefore the process deviates there. Lastly the drugs that can be ordered on the machine are always available and cannot run out, as there is always a safety stock ready.

See list of assumptions above

## To-Be process (including description of webservices)

![sone kack bild vom to be prozess](images/tobe.png?raw=true "Title")

The process starts with the customer entering. After entering the health insurance card they are greeted with the screen asking if they want to use the self-service or need personal assistance. If they choose to go with personal assistance the process directly guides them towards the manual task, where they are assisted by a pharmacy assistant or pharmacist.

When it comes to the implementation, the question whether the customer wants to use the self-service and whether he or she has a prescription is asked via a google forms. The information will then be sent to the integration system &quot;Integromat&quot; which then forwards the message to camunda triggering the token to move on. In integromat, we set up a webhook and the http request.

![sone kack bild vom integromat](images/integromat.png?raw=true "Title")


![sone kack bild vom integromat](images/integromat2.png?raw=true "Title")

![sone kack bild vom integromat](images/integromat3.png?raw=true "Title")

In case they do have a valid prescription, it needs to be scanned and the process continues. If there is an issue with the prescription again a pharmacist helps the clients out. If they choose option &quot;No&quot; for prescription then they are guided towards the next webservice which is a chatbot.


![sone kack bild vom integromat](images/chatbot.png?raw=true "Title")

From then on, the chat bot asks the client what kind of drug and how much of the drug is needed. The bot was set up with one entity and three intents. The entity drugs was configured as a manual list at the end. The final intent will call a webhook, which was implemented in the Integromat framework (see picture below). If the client choses a Non-Prescription drug the process continues and the user is able to confirm and pay the order as required. If they choose a prescription drug then the order needs to be fulfilled by a trained pharmacist, as it needs their validation regarding the prescription drug. Now if a client would indicate in the first instance, that they do not need a prescription drug, but then order a prescription drug over the chatbot, it would be detected, as there is ether no prescription document uploaded to the system and as the integromat workflow will reorganize it. All drugs who are sold in the fully automated bot are stored in a database, here in form as a excel sheet. The database has all the necessary master data in it, for example the mandatory for the prescription, yes / no. Therefore, customer safety and drug abuse is given with no excuse. The order is then confirmed and payment is ensured either through the health insurer, or via the payment webinterface. This information is then further distributed to the google sheet with the rest of the order information. As part of the integromat workflow data, like an order id and order datetime will be collected and stored in the google sheet what is representing a database for reporting and auditing reasons. The Integromat workflow in the end will respond with a web request to the camunda engine with all variables included. Lateron in the process steps a payment service webhook will be trigged with a listener in the camunda model. The workflow will then make a web request to a service task in the camunda enginge, update the specific data in the google sheet and cofirm back to the camunda engine.

![sone kack bild vom integromat](images/integromat4.png?raw=true "Title")

![sone kack bild vom integromat](images/integromat5.png?raw=true "Title")

Compared to the As-Is process, the new process offers a lot of advantages. The pharmacy will be able to function more efficiently, moreover the data that is being collected on the self-service machine will help in planning of stock and analysing trends in different seasons. Furthermore, the staff is able to really help people that are in need of advisory and not just the clients that exactly know what they want to buy.
