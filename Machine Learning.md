# Amazon Rekognition
- detect objects, people, text, scenes in images and videos using ML
- can do facial analysis and facial search to do user verification, people counting 
- Use cases:
	- labeling
	- content moderation
	- text detection
	- face detection and analysis
	- face search and verification
	- celebrity recognition
	- pathing (*example: for sports game analysis*)
# Amazon Transcribe
- convert speech to text
- uses deep learning process called automatic speech recognition (ASR) to convert speech to text
- can automatically remove Personally Identifiable Information (PII) using Redaction
- access to Automatic Language Identification for multi-lingual audio
- Use cases:
	- transcribe customer service calls
	- automate closed captioning and subtitling
	- generate metadata for media assets to create a fully searchable archive
# Amazon Polly
- *opposite of Transcribe*
- text to speech using deep learning
# Amazon Translate
- language translation
- allows to localize content - like websites and applications - for international users and to easily translate large volumes of text efficiently
# Amazon Lex & Connect
![[Pasted image 20250223160507.png]]
## Amazon Lex
- *same tech that powers Alexa*
- ASR to convert speech to text
- Natural Language Understanding to recognize the intent of text, callers
- helps build chatbots, call center bots
## Amazon Connect
- receive calls, create contact flows, cloud-based virtual contact center
- can integrate with other CRM systems or AWS services
- no upfront payments, 80% cheaper than traditional contact center solutions
# Amazon Comprehend
- for Natural Language Processing - NLP
- fully managed and serverless
- uses ML to find insights and relationships in text
	- language of text
	- extract key phrases, places, people, brands or events => *NER*
	- understand how positive or negative the text is => *sentiment analysis*
	- analyzes text using tokenization and parts of speech
	- automatically organizes a collection of text files by topic
- Sample use cases:
	- analyze customer interactions to find what leads to a positive or negative experience
	- create and group articles by topics
# Amazon SageMaker
- fully managed service to build ML models for developers / data scientists
- simplifies end-to-end ML workflow from data preparation to deployment
![[Pasted image 20250223162418.png]] 
# Amazon Forecast
- fully managed service that uses ML to deliver highly accurate forecasts
- reducing forecasting time from months to hours
- Use cases:
	- product demand pricing
	- financial planning
	- resource planning
	- ...
![[Pasted image 20250223162658.png]] 
# Amazon Kendra
- fully managed ML powered ==document search service==
- extract answers from within a document (text, pdf, HTML, PowerPoint, MS Word, ...)
- Natural language search capabilities
- learn from user interactions/feedback to promote preferred results (**incremental learning**)
- ability to manually finetune search results
![[Pasted image 20250223162929.png]]
# Amazon Personalize
- fully managed ML-service to build apps with real-time personalized recommendations
- integrates into existing websites, apps, SMS, email marketing systems, ...
- implement in days, not months => *do not need to build, train and deploy ML solutions*
- Use cases:
	- retail stores
	- media and entertainment
![[Pasted image 20250223163226.png]]
# Amazon Textract
- automatically extracts text, handwriting and data from any scanned documents using AI and ML
- extract data from forms and tables
- read and process any type of document (PDFs, images,...)
- use cases:
	- financial services => invoices, financial reports
	- healthcare => medical records, insurance claims
	- Public sector => tax forms, ID documents, passports
![[Pasted image 20250223163702.png]]
# Summary
![[Pasted image 20250223163724.png]]