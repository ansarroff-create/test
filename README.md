# test
from transformers import pipeline

model_name = "HuggingFaceTB/SmolLM2-360M-Instruct"
bot = pipeline("text-generation", model=model_name)

messages = [
    {"role": "system", "content": "You are a helpful and concise AI assistant."}
]

print("Bot: Hello! Type 'exit' to quit.")

while True:
    question = input("\nYou: ")
    if question.lower() == "exit":
        print("Bot: Goodbye!")
        break
    
    messages.append({"role": "user", "content": question})
    response = bot(messages, max_new_tokens=50)
    reply = response[0]["generated_text"][-1]["content"]
    print(f"Bot: {reply.strip()}")
    messages.append({"role": "assistant", "content": reply})
