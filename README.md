🚀 Project Objective

Modern AI assistants must convert human language into structured data that software systems can execute.
This project fine-tunes an open-source LLM to perform:

Natural Language → Structured JSON Command Extraction

🧠 Concepts Demonstrated

This project covers the complete fine-tuning lifecycle:

Instruction tuning

Dataset creation and formatting

Tokenization for causal language modeling

LoRA (Parameter Efficient Fine-Tuning)

4-bit quantization for memory-efficient training

Training using HuggingFace Trainer

Inference with a fine-tuned LoRA adapter

Model evaluation and error analysis

🏗️ Model & Training Setup
Component	Details
Base Model	TinyLlama-1.1B-Chat
Fine-Tuning Method	LoRA (PEFT)
Quantization	4-bit (BitsAndBytes)
Frameworks	HuggingFace Transformers, PEFT, Datasets
Training Environment	Google Colab GPU
Task Type	Causal Language Modeling
📂 Dataset

A custom dataset was created with examples in the format:

Instruction + Input → JSON Output

Example entry:

{
  "instruction": "Extract the structured command from the sentence and return JSON.",
  "input": "Remind me to submit the assignment tomorrow at 5 PM.",
  "output": "{\"intent\":\"set_reminder\",\"entities\":{\"person\":null,\"date\":\"tomorrow\",\"time\":\"17:00\",\"task\":\"submit the assignment\",\"location\":null,\"topic\":null,\"email_subject\":null}}"
}


The dataset was designed to:

Cover multiple intents

Include missing fields (null values)

Use consistent JSON schema

🔧 Training Approach

Instead of fine-tuning the entire model (which is computationally expensive), LoRA adapters were used to efficiently train only a small subset of parameters.

This allows:

Faster training

Lower GPU memory usage

Behavior specialization without overwriting base knowledge

📊 Results

After fine-tuning:

The model learned to output structured JSON instead of conversational text.

It correctly identified intents and extracted key entities.

Some base-model tendencies remained (extra fields or alternate intent names), demonstrating real-world fine-tuning challenges.

🧪 Example Inference

Input:

"Book a haircut appointment this Sunday at 4 PM"

Model Output:

{
  "intent": "book_event",
  "entities": {
    "person": "haircut appointment",
    "date": "Sunday",
    "time": "16:00",
    "task": null,
    "location": null,
    "topic": null,
    "email_subject": null
  }
}

📘 What This Project Teaches

This project demonstrates practical understanding of:

How LLMs are fine-tuned for specific behaviors

How structured outputs can be enforced

How LoRA enables efficient adaptation of large models

The importance of dataset design in model performance

🔮 Future Improvements

Expanding dataset size for stronger schema control

Adding validation metrics for structured accuracy

Introducing negative examples to prevent hallucinated fields

Evaluating model performance on unseen real-world instructions

🏁 Conclusion

This project shows how LLMs can be specialized beyond chat applications into structured AI systems capable of powering assistants, automation tools, and intelligent software workflows.
