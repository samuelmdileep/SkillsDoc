# 🧠 SkillDocs - Your Smart Resume Companion

SkillDocs is a web platform that allows users to **upload, manage, and showcase their skills and certifications**. It integrates with Firebase and includes an **AI-powered resume generator** using a fine-tuned T5 model.

---

## 🚀 Features

- 🔐 Google Sign-In authentication  
- 📄 Upload and manage your **skills** and **certifications**  
- 🧠 AI Resume Generator (T5 model fine-tuned on resume data)  
- 🖼 Upload profile picture  
- 🔥 Firebase integration  

---

## 📁 Project Structure

📦 SkillDocs
├── index.html
├── profile.html
├── resume.html
├── /scripts/
│ ├── firebase-config.js
│ ├── auth.js
│ ├── resumeGen.js
├── /models/
│ └── resume_t5_model/

python
Copy code

---

## 🧠 T5 Model Training (Python)

```python
from transformers import T5Tokenizer, T5ForConditionalGeneration
from datasets import Dataset

tokenizer = T5Tokenizer.from_pretrained("t5-small")
dataset = Dataset.from_list(data)

def preprocess(example):
    input_enc = tokenizer(example["input"], padding="max_length", truncation=True, max_length=64)
    output_enc = tokenizer(example["output"], padding="max_length", truncation=True, max_length=64)
    input_enc["labels"] = output_enc["input_ids"]
    return input_enc

tokenized_dataset = dataset.map(preprocess)
✅ Download the final model: resume_t5_model.zip and place it in /models/

🖥️ How to Run Locally
Clone the repo:

bash
Copy code
git clone https://github.com/samuelmdileep/SkillDocs.git
cd SkillDocs
Open index.html using Live Server or Python local server.

Connect Firebase in firebase-config.js.

Ensure model is available in models/.

📅 Future Plans
📄 Multiple Resume Templates

🔍 Skill Suggestions with GPT

📤 Export to PDF

📝 Editable Skill Tags

📬 Contact
Samuel M Dileep
📧 samuelmdileep@gmail.com
📱 +91 80752 58045
IEEE/ISTE/IEDC Member

LinkedIn
https://www.linkedin.com/in/samuel-m-dileep-b84960314/

📬 Contact
📧 Email: samuelmdileep@gmail.com
📱 Phone: +91 80752 58045
