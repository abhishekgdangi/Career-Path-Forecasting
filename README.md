\documentclass[11pt,a4paper]{article}

% ---------- Packages ----------
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage[margin=2.2cm]{geometry}
\usepackage{amsmath}
\usepackage{booktabs}
\usepackage{tabularx}
\usepackage{array}
\usepackage[table]{xcolor}
\usepackage{enumitem}
\usepackage{titlesec}
\usepackage{fancyhdr}
\usepackage{tcolorbox}
\usepackage[hidelinks]{hyperref}

% ---------- Colors ----------
\definecolor{navy}{HTML}{1F3A5F}
\definecolor{teal}{HTML}{2A9D8F}
\definecolor{lightteal}{HTML}{EAF4F3}

% ---------- Styling ----------
\titleformat{\section}{\Large\bfseries\color{navy}}{\thesection.}{0.6em}{}
\titleformat{\subsection}{\large\bfseries\color{teal}}{}{0em}{}
\titlespacing*{\section}{0pt}{16pt}{6pt}
\setlength{\parindent}{0pt}
\setlength{\parskip}{6pt}
\setlist[itemize]{itemsep=2pt,topsep=2pt}
\renewcommand{\arraystretch}{1.3}

\pagestyle{fancy}
\fancyhf{}
\fancyfoot[L]{\small\color{gray}Career Path Forecasting -- Project Explained}
\fancyfoot[R]{\small\color{gray}Page \thepage}
\renewcommand{\headrulewidth}{0pt}

\newtcolorbox{keybox}{colback=lightteal,colframe=teal,boxrule=0pt,
  leftrule=3pt,arc=0pt,left=8pt,top=5pt,bottom=5pt}

\newcolumntype{L}[1]{>{\raggedright\arraybackslash}p{#1}}

\begin{document}

% ---------- Title ----------
\begin{center}
  {\Huge\bfseries\color{navy} Career Path Forecasting}\\[6pt]
  {\Large\color{teal} Project Explained in Simple Words}\\[10pt]
  Dayananda Sagar College of Engineering, CSE (Data Science)\\
  Abhishek G Dangi, Sambhram S Naregal, Amarnath V, K Yuvraj Sundaram
\end{center}
\vspace{4pt}

% ---------- 1 ----------
\section{What Is This Project?}
\begin{keybox}
\textbf{It is a smart app that looks at a student's profile (marks, internships, skills, interests) and predicts what they are most likely to do after college: get a job (placement), go for higher studies, or start a startup.} It also gives each student a single score out of 10, called the API score, that shows overall readiness and not just marks.
\end{keybox}

\textbf{Why did we make it?} Most colleges judge students only by CGPA. But a student with internships, projects, certificates and leadership can be more ready for the real world than someone with only good marks. Many students are also confused after final year: \emph{``Should I take a job, study more, or start something?''} Our app helps answer this using data.

% ---------- 2 ----------
\section{What Does the App Do?}
\begin{tabularx}{\textwidth}{L{3.6cm} X X}
\toprule
\rowcolor{navy}\textbf{\color{white}Part} & \textbf{\color{white}You give} & \textbf{\color{white}You get} \\
\midrule
\textbf{Tab 1: Career Path Forecasting} (for colleges) &
Excel file of many students (CGPA, internship, research papers, startup experience, startup skills, programming languages, coding) &
Predicted outcome for each student, a bar chart of the groups, and a CSV download \\
\addlinespace
\textbf{API Score Calculator} (inside Tab 1) &
CGPA, paid and unpaid internships, courses, certificates &
Score out of 10 with a short comment \\
\addlinespace
\textbf{Tab 2: Personalized Recommendation} (for one student) &
12 sliders: CGPA, technical skills, communication, internships, projects, extracurriculars, leadership, creativity, analytical thinking, research, business and technical interest &
Chance (\%) of each path, top recommendation, influence chart and tips \\
\bottomrule
\end{tabularx}

% ---------- 3 ----------
\section{Tools and Data Used}
\begin{tabularx}{\textwidth}{L{4cm} X}
\toprule
\textbf{Tool} & \textbf{Why we used it} \\
\midrule
Python & Main programming language \\
Pandas, NumPy & Read Excel files and prepare data \\
Scikit-learn & Build and train the machine-learning models \\
Random Forest & Main model: accurate, stable, handles many inputs \\
Joblib, Pickle & Save the trained model so it can be reused \\
Streamlit & Build the web app with upload button, sliders and tabs \\
Matplotlib, Seaborn, Plotly & Charts and graphs \\
\bottomrule
\end{tabularx}

\subsection*{The Data}
\begin{itemize}
  \item \textbf{Student table:} USN, name, CGPA, post-graduation plan, co-curricular activities, recognitions, workshops, entrepreneurship experience, startup skills, programming language, coding level, internship, research papers.
  \item \textbf{Target (what we predict):} Placement, Higher Studies or Startup.
  \item \textbf{Files:} \texttt{datayesno.xlsx} (1000 students) for training and testing, \texttt{datatest.xlsx} (16 students) and \texttt{datatest2.xlsx} (29 students) for trying the app.
  \item The research paper reports a dataset of more than 3000 students. The script \texttt{data.py} also creates a practice dataset of 200 students.
\end{itemize}

% ---------- 4 ----------
\section{How Does the Model Work?}
\begin{keybox}
\textbf{Random Forest = a team of many decision trees voting.} Imagine asking 100 senior students for advice. Each looks at your profile differently and gives an answer. The answer with the most votes wins. One person can be wrong, but 100 voting together is much more reliable.
\end{keybox}

\subsection*{Step by Step}
\begin{enumerate}[itemsep=2pt]
  \item \textbf{Collect data} about past students and what they actually chose.
  \item \textbf{Clean it:} remove empty rows, convert Yes/No to 1/0, encode labels as numbers.
  \item \textbf{Scale the numbers} so a 0--100 slider and a 0--5 count are treated fairly.
  \item \textbf{Split the data:} 80\% to teach the model, 20\% to test it.
  \item \textbf{Train} the Random Forest (100 trees).
  \item \textbf{Save} the model to a file (\texttt{.pkl} or \texttt{.joblib}).
  \item \textbf{Use it in the app:} user gives input, model predicts, app shows the result.
\end{enumerate}

\subsection*{Two Models in the Project}
\begin{tabularx}{\textwidth}{L{4.3cm} L{2.6cm} X}
\toprule
\textbf{Model file} & \textbf{Used in} & \textbf{Inputs and output} \\
\midrule
\texttt{student\_placement\_model.pkl} & Tab 1 (Excel) & 7 inputs (CGPA, internship, research papers, entrepreneurship experience, startup skills, programming languages, coding). Output: Placement / Higher Studies / Startup. \\
\addlinespace
\texttt{career\_model.joblib} + \texttt{career\_scaler.joblib} & Tab 2 (sliders) & 12 inputs from the sliders. Output: Entrepreneurship / Higher Studies / Job Placement, with a percentage for each. \\
\bottomrule
\end{tabularx}

% ---------- 5 ----------
\section{What Is the API Score?}
API stands for \textbf{Academic Performance Indicator}. It is one number out of 10 showing overall readiness, not just marks. The calculator in the app adds points like this:

\begin{center}
\begin{tabularx}{0.95\textwidth}{L{4.2cm} c X}
\toprule
\textbf{Part} & \textbf{Max points} & \textbf{How it is counted} \\
\midrule
CGPA & 3 & $\dfrac{\text{CGPA}}{10} \times 3$ \\
Internships & 4 & Paid = 2 points, unpaid = 1 point each \\
Courses & 2 & IIT 0.5, NIT 0.4, Industry 0.3, Other 0.2 per course \\
Certificates & 1 & 0.5 per certificate \\
\midrule
\textbf{Total} & \textbf{10} & 8.5+ Excellent, 7+ Good, 5+ Fair, below 5 Needs improvement \\
\bottomrule
\end{tabularx}
\end{center}

In formula form:
\[
\text{API} = \min\!\left(\tfrac{\text{CGPA}}{10}\times 3,\,3\right) + \min(2P + U,\,4) + \min(C,\,2) + \min(0.5\,N,\,1)
\]
where $P$ = paid internships, $U$ = unpaid internships, $C$ = weighted course points, and $N$ = number of certificates.

% ---------- 6 ----------
\section{How Good Are the Results?}
These values are reported in our research paper.

\begin{center}
\begin{tabularx}{0.95\textwidth}{L{4cm} L{3.6cm} c X}
\toprule
\textbf{Task} & \textbf{Measure} & \textbf{Result} & \textbf{Simple meaning} \\
\midrule
API score prediction & $R^2$ & 0.89 & Explains about 89\% of the score pattern \\
 & RMSE / MAE & 0.48 / 0.37 & Off by less than half a point on average \\
Career path prediction & Accuracy & 86.3\% & About 86 of 100 predictions are correct \\
 & Precision / Recall / F1 & 84.7 / 85.1 / 84.9\% & Balanced across paths \\
\bottomrule
\end{tabularx}
\end{center}

% ---------- 7 ----------
\section{Project Folder Files}
\begin{tabularx}{\textwidth}{L{5.2cm} X}
\toprule
\textbf{File} & \textbf{What it does} \\
\midrule
\texttt{frontend.py} & \textbf{Main app.} Run with \texttt{streamlit run frontend.py} \\
\texttt{data.py} & Creates practice data and trains a test Random Forest \\
\texttt{app.py}, \texttt{apptest.py} & Test scripts for predictions \\
\texttt{appp.py}, \texttt{streamlit.py} & Earlier versions of the app \\
\texttt{*.pkl}, \texttt{*.joblib} & Saved models, scaler, encoder, feature names \\
\texttt{datayesno.xlsx}, \texttt{datatest*.xlsx} & Student datasets \\
\texttt{Career\_Input\_Guidelines.pdf} & Guide for filling the sliders honestly \\
Research paper (\texttt{.docx}) & Written report of the project \\
\bottomrule
\end{tabularx}

% ---------- 8 ----------
\section{Limitations and Future Work}
\begin{itemize}
  \item Part of the training data is \textbf{synthetic}, so the model learns the patterns built into it. Real student data would be more trustworthy.
  \item Tab 2 uses \textbf{self-rated} inputs, so honest answers matter.
  \item The prediction is a \textbf{guide, not a final decision}.
  \item Future work: larger real datasets, more features (soft skills, certificate quality), and a mobile-friendly version for placement cells.
\end{itemize}

% ---------- 9 ----------
\section{One-Line Summary}
\begin{keybox}
\emph{``We built a Streamlit web app that uses a Random Forest machine-learning model to predict whether a student will go for placement, higher studies or a startup, and calculates an API score out of 10, giving students and colleges data-driven career guidance instead of relying only on CGPA.''}
\end{keybox}

\end{document}
