# 🧠 SkillDocs - Your Smart Resume Companion

SkillDocs is a web platform that allows users to **upload, manage, and showcase their skills and certifications**. It integrates with Firebase for user authentication and data storage, and includes an **AI-powered resume generator** using a fine-tuned T5 model. Users can build a strong profile, generate personalized resumes, and manage skills — all from a clean and responsive UI.

---

## 🚀 Features

- 🔐 Google Sign-In authentication
- 📄 Upload and manage your **skills** and **certifications**
- 🖼 Upload and change profile picture with compression
- 🧑‍💼 Update personal details like name, college, course, department
- 🧠 AI Resume Generator (T5 model fine-tuned on real resume data)
- 🖥 Responsive web interface (mobile-friendly)
- 📁 Firebase-integrated file structure and storage
- ✅ Delete confirmation modals with toast-style success/error feedback

---

## 🛠️ Technologies Used

| Tech        | Purpose                           |
|-------------|-----------------------------------|
| **Firebase** | Authentication & Firestore storage |
| **HTML + JS** | UI and dynamic logic              |
| **Tailwind CSS** | Styling and responsiveness      |
| **T5 Transformer** | AI Resume Text Generation     |
| **Google Colab** | Model training & fine-tuning    |

---

## 📁 Project Structure

📦 SkillDocs
├── index.html # Main dashboard page
├── profile.html # User profile & settings
├── resume.html # Resume generator UI
├── upload.html # Skill/certification upload form
├── /scripts/
│ ├── firebase-config.js # Firebase init with modular SDK
│ ├── auth.js # Auth logic (sign in/out)
│ ├── profile.js # Profile update, picture upload
│ ├── skills.js # Upload & display skills
│ ├── resumeGen.js # Resume generation from T5 model
├── /styles/
│ └── tailwind.css # Tailwind base styling
├── /models/
│ └── resume_t5_model/ # AI model saved locally (or API connected)

yaml
Copy code

---

## 🧠 Resume Generator - Model Training (T5)

We fine-tuned a [`t5-small`](https://huggingface.co/t5-small) model using a custom dataset of 150+ resume entries in this format:

```json
{
  "input": "B.Tech EEE student skilled in Flutter, Firebase, and IoT",
  "output": "An enthusiastic Electrical Engineering student with experience in Flutter app development, Firebase integration, and IoT systems."
}
🔧 Training Process (Colab Notebook)
python
Copy code
from transformers import T5Tokenizer, T5ForConditionalGeneration, TrainingArguments, Trainer
from datasets import Dataset

# Load and tokenize data
tokenizer = T5Tokenizer.from_pretrained("t5-small")
dataset = Dataset.from_list(data)

def preprocess(example):
    input_enc = tokenizer(example["input"], padding="max_length", truncation=True, max_length=64)
    output_enc = tokenizer(example["output"], padding="max_length", truncation=True, max_length=64)
    input_enc["labels"] = output_enc["input_ids"]
    return input_enc

tokenized_dataset = dataset.map(preprocess)

# Split dataset
train_test = tokenized_dataset.train_test_split(test_size=0.1)
train_dataset = train_test["train"]
eval_dataset = train_test["test"]

# Train the model
model = T5ForConditionalGeneration.from_pretrained("t5-small")
training_args = TrainingArguments(output_dir="./resume_t5_model", per_device_train_batch_size=8, learning_rate=3e-4, num_train_epochs=5)
trainer = Trainer(model=model, args=training_args, train_dataset=train_dataset)
trainer.train()

# Save model
model.save_pretrained("./resume_t5_model")
tokenizer.save_pretrained("./resume_t5_model")
✅ Download the final model: resume_t5_model.zip (also used in frontend)

⚙️ How to Run Locally
Clone the repo:

bash
Copy code
git clone https://github.com/yourusername/SkillDocs.git
cd SkillDocs
Open the index.html using Live Server or a local server.

Connect Firebase project in firebase-config.js.

Ensure the T5 model is either hosted via API or pre-downloaded.

📅 Future Plans
📄 Multiple Resume Templates

🧠 Smart Recommendations using GPT (e.g., Skill Suggestions)

📦 Export to PDF

🌐 PWA Support for offline use

📝 Editable Skill Tags & Category Filters

🤝 Credits
Developed by Samuel M Dileep

IEEE/ISTE/IEDC Member

LinkedIn
https://www.linkedin.com/in/samuel-m-dileep-b84960314/

📬 Contact
📧 Email: samuelmdileep@gmail.com
📱 Phone: +91 80752 58045