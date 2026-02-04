# Instructor Guide: Using Pre-Trained Models and SDKs

## Module Overview

In this module, learners leverage pre-trained AI services and SDKs to implement language, vision, and recommendation features. The focus shifts from understanding the underlying theory of ML to the practical application of "Model as a Service" (MaaS). Students will learn to integrate powerful, production-ready intelligence into web applications using official Software Development Kits (SDKs) rather than building models from scratch.

## Learning Objectives

By the end of this session, students will be able to:

* **Implement AI functionality** using pre-trained SDKs and APIs to enhance web features.
* **Differentiate** between raw API calls (`fetch`) and SDK methods, articulating the benefits of using official libraries for error handling and type safety.
* **Integrate** distinct AI capabilities—specifically text generation (via OpenAI) and object detection (via TensorFlow.js)—into an existing codebase.

## Session Pacing Guide (120 Minutes total)

| Duration | Segment | Instructor Action |
| --- | --- | --- |
| **20 min** | **The "Model as a Service" Paradigm** | Introduce the concept of MaaS. Use the "Pizza Delivery vs. Farming" analogy. Discuss the trade-offs of Build vs. Buy. |
| **20 min** | **APIs vs. SDKs** | Live Code Comparison: Show a raw `fetch` call with complex headers alongside a clean SDK method call. Highlight the readability difference. |
| **25 min** | **Language Features (OpenAI SDK)** | Demo: Sentiment Analysis. Show how to use the `system` role to constrain the AI's output to specific JSON formats. |
| **25 min** | **Vision Features (TensorFlow.js)** | Demo: Object Detection. Load the `coco-ssd` model in a blank HTML page and detect objects in a static image. |
| **30 min** | **Lab: Adding AI Sentiment Features** | Facilitate the lab. Help students implement a "Review Analyzer" using the OpenAI Node.js SDK. |

---

## Delivery Notes & Teaching Tips

### 1. The "Pizza Delivery" Analogy (MaaS)

* **Concept:** Beginners often feel like "cheaters" for not training their own models.
* **The Analogy:**
* **Training a Model:** Like farming wheat, growing tomatoes, and raising cows just to make a pizza. (Necessary for researchers, inefficient for hungry people).
* **Pre-trained Model (MaaS):** Like calling a pizza place. You get a professional-grade pizza in 20 minutes.


* **Takeaway:** Your value as a developer is not *making* the pizza, it's *serving* it to the customer in a nice restaurant (The Web App).

### 2. SDK vs. Raw API (The "Cake Mix" Analogy)

* **Visual Aid:** Split the screen.
* Left side: A raw `fetch` request with manual error handling, `JSON.stringify`, and header management.
* Right side: `openai.chat.completions.create()`.


* **Analogy:**
* **Raw API:** Baking a cake from scratch (flour, eggs, baking soda). You have total control but can easily mess up the ratios.
* **SDK:** A box cake mix. It has the error handling and configurations pre-mixed. You just add water (Arguments) and bake.



### 3. Prompt Engineering as "Coding"

* **Tip:** Emphasize that in the SDK `messages` array, the **System Prompt** is essentially code.
* **Demo:** Show how changing the system prompt from "You are a helpful assistant" to "You are a JSON generator that only outputs { sentiment: string }" changes the entire behavior of the app from a chatbot to a utility function.

---

## Lab Guide: Adding AI Sentiment Features

**Lab Objective:** Add a text-generation or sentiment-analysis feature to a web app using a pre-trained model.

### Setup

* **Starter Code:** A simple "Product Review" React/Node application.
* **Tools:** Node.js, OpenAI SDK.

### Common Student Issues & Solutions

* **Issue:** "I'm getting `ImportError` or `require is not defined`."
* *Solution:* Check if they are using ES Modules (`import`) vs CommonJS (`require`). Ensure `package.json` has `"type": "module"` or they stick to consistent syntax.


* **Issue:** The AI replies with "Sure! The sentiment is Positive." instead of just "Positive."
* *Solution:* This breaks the code logic. Teach them to refine the prompt: *"Do not output any conversational filler. Output only the label."* or use `temperature: 0`.


* **Issue:** "My TensorFlow model (Vision) works on the first click but crashes on the second."
* *Solution:* They might be reloading the model every time the button is clicked (heavy operation). Teach them to load the model *once* when the component mounts (using `useEffect`) and store it in a variable/state.



### Debrief Questions

At the end of the lab, ask:

1. "Why is the SDK method `.create()` easier to use than `fetch()`?" (Auto-completion/IntelliSense, error handling).
2. "In the vision example, the model was running in your browser. In the text example, it ran on a server. What is the privacy difference?" (Vision data stayed local; Text data was sent to OpenAI).

---

## Resources for the Instructor

* **Reference:** [OpenAI Node.js SDK](https://github.com/openai/openai-node)
* **Reference:** [TensorFlow.js COCO-SSD Demo](https://github.com/tensorflow/tfjs-models/tree/master/coco-ssd)
* **AI Prompt Bank:**
* *"What is the difference between a 'System' message and a 'User' message in the OpenAI API?"*
* *"Write a prompt that extracts the date and time from this email: 'Let's meet next Tuesday at 4pm'."*