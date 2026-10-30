<div align="center">

# 🎓 Career Path Forecasting

### Predict what a student will do after college: **Job**, **Higher Studies** or **Startup**

*Machine-learning powered career guidance, built with Python, Scikit-learn and Streamlit.*

![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-App-FF4B4B?logo=streamlit&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-Random%20Forest-F7931E?logo=scikitlearn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data-150458?logo=pandas&logoColor=white)
![Status](https://img.shields.io/badge/Status-Prototype-2A9D8F)

</div>

---

## 📌 About the Project

Most colleges judge students only by **CGPA**. But internships, projects, certificates, leadership and interests matter just as much for real-world success. On top of that, many final-year students are confused: *"Should I take a job, study more, or start something of my own?"*

**Career Path Forecasting** looks at a student's complete profile and:

- 🔮 **Predicts** the most likely career path (Placement / Higher Studies / Startup)
- 📊 **Calculates an API Score** (Academic Performance Indicator) out of 10 that shows overall readiness
- 💡 **Explains** which factors influenced the prediction and gives improvement tips

> Built as a research project at **Dayananda Sagar College of Engineering**, Dept. of CSE (Data Science).

---

## ✨ Features

| Feature | Description |
|---|---|
| 📁 **Bulk Prediction** | Upload an Excel file with many students and get a prediction for each one |
| 📈 **Outcome Chart** | Interactive bar chart showing how many students fall in each career path |
| 🧮 **API Score Calculator** | One score out of 10 from CGPA, internships, courses and certificates |
| 🧠 **Personalized Recommendation** | 12 sliders about yourself, get the % chance of each career path |
| 🔍 **Explainability** | Top influencing factors shown in a chart, with suggestions |
| ⬇️ **Downloads** | Export predictions and insights as CSV |
| 📘 **Input Guidelines** | A PDF that helps students rate themselves honestly |

---

## 🖥️ How the App Works

The app has **two tabs**:

### Tab 1: Career Path Forecasting (for colleges and teachers)
1. Upload an Excel file of students
2. The model predicts **Placement / Higher Studies / Startup** for every student
3. See the distribution chart and download the results
4. Use the built-in **API Score Calculator** for any single student

### Tab 2: Personalized Career Recommendation (for one student)
1. Move the sliders (CGPA, technical skills, communication, leadership, creativity, etc.)
2. Click **Analyze Career Path**
3. Get the probability of each path, the top recommendation and tips

---

## 🧮 API Score (out of 10)

| Component | Max Points | How it is counted |
|---|:---:|---|
| 🎓 CGPA | 3 | `CGPA / 10 × 3` |
| 💼 Internships | 4 | Paid = 2 points, Unpaid = 1 point (each) |
| 📚 Courses | 2 | IIT `0.5`, NIT `0.4`, Industry `0.3`, Other `0.2` (per course) |
| 🏅 Co-curricular certificates | 1 | `0.5` per certificate |
| **Total** | **10** | **8.5+** Excellent · **7+** Good · **5+** Fair · **<5** Needs improvement |

---

## 🤖 How the Model Works

The project uses a **Random Forest Classifier**, which is a team of 100 decision trees that vote on the final answer. One tree can be wrong, but many trees voting together are far more reliable.

```
Raw Data → Cleaning → Encoding & Scaling → Train / Test Split (80/20) → Random Forest → Saved Model → Streamlit App
```

The project has **two trained models**:

| Model | Used in | Inputs | Output |
|---|---|---|---|
| `student_placement_model.pkl` | Tab 1 (Excel upload) | CGPA, internship, research papers, entrepreneurship experience, startup skills, programming languages, coding | Placement / Higher Studies / Startup |
| `career_model.joblib` + `career_scaler.joblib` | Tab 2 (sliders) | 12 profile features | Entrepreneurship / Higher Studies / Job Placement, with probabilities |

---

## 📊 Results (from the research paper)

| Task | Metric | Result |
|---|---|:---:|
| API score prediction | R² Score | **0.89** |
| | RMSE / MAE | 0.48 / 0.37 |
| Career path prediction | Accuracy | **86.3%** |
| | Precision / Recall / F1 | 84.7% / 85.1% / 84.9% |

---

## 🛠️ Tech Stack

- **Language:** Python
- **Machine Learning:** Scikit-learn (Random Forest, StandardScaler, LabelEncoder)
- **Data:** Pandas, NumPy, OpenPyXL
- **Visualization:** Matplotlib, Seaborn, Plotly
- **Web App:** Streamlit
- **Model Storage:** Joblib, Pickle

---

## 📂 Project Structure

```
Career-Path-Forecasting/
│
├── frontend.py                  # ⭐ Main Streamlit app (run this)
├── data.py                      # Generates sample data and trains a test model
├── app.py / apptest.py          # Scripts to test predictions
├── appp.py / streamlit.py       # Earlier versions of the app
│
├── student_placement_model.pkl  # Model for Tab 1
├── label_encoder.pkl            # Converts labels to numbers and back
├── career_model.joblib          # Model for Tab 2
├── career_scaler.joblib         # Scaler for Tab 2 inputs
├── feature_names.joblib         # Feature names for Tab 2
│
├── datayesno.xlsx               # Main dataset (1000 students)
├── datatest.xlsx                # Sample test file (16 students)
├── datatest2.xlsx               # Sample test file (29 students)
│
├── Career_Input_Guidelines.pdf  # How to rate yourself on the sliders
└── Career Path Forecasting Research Paper.docx
```

---

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/<your-username>/Career-Path-Forecasting.git
cd Career-Path-Forecasting
```

### 2. (Optional) Create a virtual environment
```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
```

### 3. Install dependencies
```bash
pip install streamlit pandas numpy scikit-learn joblib matplotlib seaborn plotly openpyxl
```

### 4. Run the app
```bash
streamlit run frontend.py
```

The app opens in your browser at `http://localhost:8501`.

> ⚠️ **Tip:** The models were trained with scikit-learn **1.6.1**. If you see a version warning, install it with `pip install scikit-learn==1.6.1`.

---

## 📁 Excel File Format (Tab 1)

Your uploaded file must contain these columns. Spelling matters, so keep them exactly as written:

| Column | Value |
|---|---|
| `cgpa` | Number (e.g. 8.5) |
| `internship` | `yes` / `no` |
| `research papers` | `yes` / `no` |
| `enterpreunership experience` | `yes` / `no` |
| `skills for stratup` | `yes` / `no` |
| `programming languages` | Number |
| `coding` | Number |

Try it with the included `datatest.xlsx` or `datatest2.xlsx` files, or use `datayesno.xlsx` as a reference.

---

## ⚠️ Limitations

- Part of the training data is **synthetic (computer-generated)**, so results depend on the patterns built into it. Real student data would improve reliability.
- Tab 2 uses **self-rated** inputs, so honest answers matter (see the guidelines PDF).
- Predictions are a **guide, not a final decision**.

## 🔮 Future Scope

- Train on larger, real-world student datasets
- Add more features such as soft skills and certificate quality
- Add a student login and history
- Mobile-friendly design for placement cells and institutions

---

## 👨‍💻 Team

| Name | Department |
|---|---|
| **Abhishek G Dangi** | CSE (Data Science), DSCE Bengaluru |
| **Sambhram S Naregal** | CSE (Data Science), DSCE Bengaluru |
| **Amarnath V** | CSE (Data Science), DSCE Bengaluru |
| **K Yuvraj Sundaram** | CSE (Data Science), DSCE Bengaluru |

🙏 *Guided by **Dr. Aarathi S** and HOD **Dr. Rashmi S**, Dayananda Sagar College of Engineering.*

---

<div align="center">

⭐ **If you like this project, give it a star!** ⭐

</div>
