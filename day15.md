# Daily Diary – Day 15
`Date : 9/7/26`
**Subject:** Python Programming
#### **Topic Covered:** Streamlit – Installation, Text Elements, Widgets, Layout, Charts, DataFrames, File Upload & Mini Projects

---

## 1. What is Streamlit? (Brief Theory)
**Streamlit** is an open-source Python library that lets you build **interactive web apps** directly from Python scripts — no HTML, CSS, or JavaScript required. It is widely used for building data science dashboards, ML model demos, and data visualization apps.

**Key Features:**
- Write pure Python → get a web app instantly
- Runs in browser
- Hot reloads on every save
- Works perfectly with Pandas, NumPy, and Matplotlib

```bash
# Installation
pip install streamlit

# Run an app
streamlit run app.py
```

---

## 2. First Streamlit App

```python
# app.py
import streamlit as st

st.title("My First Streamlit App")
st.write("Hello, welcome to Streamlit!")
```

```bash
streamlit run app.py
# Opens automatically at http://localhost:8501
```

---

## 3. Text Elements

**Theory:** Streamlit provides multiple functions to display different types of text with different styling.

```python
import streamlit as st

st.title("This is a Title")              # largest heading
st.header("This is a Header")            # second level
st.subheader("This is a Subheader")      # third level
st.text("This is plain text")            # plain monospace text
st.write("This is write — most flexible") # markdown + data + charts
st.markdown("**Bold**, *Italic*, `code`") # markdown support
st.caption("This is a small caption")    # small grey text
st.code("print('Hello World')", language='python')  # code block
```

---

## 4. Displaying Data

```python
import streamlit as st
import pandas as pd
import numpy as np

# Display a DataFrame
df = pd.DataFrame({
    "Name":   ["Bhawna", "Taman", "Ram", "Sham", "Gita"],
    "Marks":  [85, 72, 90, 45, 78],
    "Grade":  ["A", "B", "A", "D", "B"]
})

st.dataframe(df)                      # interactive scrollable table
st.table(df)                          # static table
st.write(df)                          # also works for DataFrames

# Display metrics
st.metric(label="Total Students", value=5)
st.metric(label="Average Marks",  value="74.0", delta="5.0")
st.metric(label="Top Score",      value=90, delta="+10")
```

---

## 5. Input Widgets

**Theory:** Widgets let users interact with the app. Every widget returns a value that you can use in your Python code.

```python
import streamlit as st

# Text input
name = st.text_input("Enter your name:")
st.write(f"Hello, {name}!")

# Number input
age = st.number_input("Enter your age:", min_value=1, max_value=100, value=21)
st.write(f"Your age is: {age}")

# Slider
marks = st.slider("Select marks:", min_value=0, max_value=100, value=50)
st.write(f"Marks selected: {marks}")

# Selectbox (dropdown)
course = st.selectbox("Choose a course:", ["Python", "Java", "C++", "Machine Learning"])
st.write(f"You selected: {course}")

# Multiselect
skills = st.multiselect("Select your skills:", ["Python", "SQL", "Excel", "Tableau", "PowerBI"])
st.write(f"Your skills: {skills}")

# Radio button
gender = st.radio("Select gender:", ["Male", "Female", "Other"])
st.write(f"Gender: {gender}")

# Checkbox
agree = st.checkbox("I agree to the terms and conditions")
if agree:
    st.write("Thank you for agreeing!")

# Button
if st.button("Click Me"):
    st.write("Button was clicked!")

# Text area
feedback = st.text_area("Write your feedback:")
st.write(f"Feedback: {feedback}")

# Date input
import datetime
dob = st.date_input("Select your date of birth:", datetime.date(2000, 1, 1))
st.write(f"DOB: {dob}")
```

---

## 6. Layout – Columns & Sidebar

```python
import streamlit as st

# Columns – side by side layout
col1, col2, col3 = st.columns(3)

with col1:
    st.header("Column 1")
    st.write("Content in col 1")
    st.button("Button 1")

with col2:
    st.header("Column 2")
    st.write("Content in col 2")
    st.button("Button 2")

with col3:
    st.header("Column 3")
    st.write("Content in col 3")
    st.button("Button 3")

# Sidebar
st.sidebar.title("Sidebar Menu")
st.sidebar.selectbox("Navigate:", ["Home", "About", "Contact"])
st.sidebar.slider("Filter by Age:", 0, 100, 25)
option = st.sidebar.radio("Choose option:", ["Option 1", "Option 2"])
st.write(f"Selected: {option}")
```

---

## 7. Expander & Tabs

```python
import streamlit as st

# Expander – show/hide content
with st.expander("Click to see more details"):
    st.write("This content is hidden by default.")
    st.write("You can put any content inside an expander.")

# Tabs
tab1, tab2, tab3 = st.tabs(["Home", "Data", "Charts"])

with tab1:
    st.write("Welcome to Home tab!")

with tab2:
    st.write("Here is your data!")

with tab3:
    st.write("Charts go here!")
```

---

## 8. Charts in Streamlit

```python
import streamlit as st
import pandas as pd
import numpy as np

# Line Chart
chart_data = pd.DataFrame(
    np.random.randn(20, 3),
    columns=["Python", "Java", "C++"]
)
st.line_chart(chart_data)

# Bar Chart
st.bar_chart(chart_data)

# Area Chart
st.area_chart(chart_data)

# Matplotlib chart inside Streamlit
import matplotlib.pyplot as plt

fig, ax = plt.subplots()
ax.bar(["Bhawna", "Taman", "Ram", "Sham"], [85, 72, 90, 45], color="skyblue")
ax.set_title("Student Marks")
ax.set_xlabel("Student")
ax.set_ylabel("Marks")
st.pyplot(fig)
```

---

## 9. File Upload

```python
import streamlit as st
import pandas as pd

uploaded_file = st.file_uploader("Upload a CSV file", type=["csv"])

if uploaded_file is not None:
    df = pd.read_csv(uploaded_file)
    st.write("File uploaded successfully!")
    st.dataframe(df)
    st.write("Shape:", df.shape)
    st.write("Columns:", list(df.columns))
    st.bar_chart(df.select_dtypes(include='number').iloc[:10])
```

---

## 10. Messages & Alerts

```python
import streamlit as st

st.success("This is a success message!")
st.error("This is an error message!")
st.warning("This is a warning!")
st.info("This is an info message!")
st.exception(ValueError("This shows an exception with traceback"))
```

---

## 11. Session State (Remember Values)

**Theory:** By default, Streamlit re-runs the whole script on every interaction. `st.session_state` stores values between reruns.

```python
import streamlit as st

if "count" not in st.session_state:
    st.session_state.count = 0

if st.button("Increment"):
    st.session_state.count += 1

if st.button("Reset"):
    st.session_state.count = 0

st.write(f"Count: {st.session_state.count}")
```

---

## 12. Mini Projects

### Project 1 – Student Grade Calculator
```python
import streamlit as st

st.title("Student Grade Calculator")

name   = st.text_input("Enter Student Name:")
maths  = st.slider("Maths Marks:",   0, 100, 50)
sci    = st.slider("Science Marks:", 0, 100, 50)
eng    = st.slider("English Marks:", 0, 100, 50)

if st.button("Calculate"):
    total   = maths + sci + eng
    average = total / 3

    if average >= 85:
        grade = "A"
    elif average >= 70:
        grade = "B"
    elif average >= 55:
        grade = "C"
    elif average >= 33:
        grade = "D"
    else:
        grade = "Fail"

    st.success(f"Student: {name}")
    st.metric("Total",   total)
    st.metric("Average", f"{average:.2f}")
    st.metric("Grade",   grade)
```

---

### Project 2 – CSV Data Explorer
```python
import streamlit as st
import pandas as pd

st.title("CSV Data Explorer")
st.sidebar.header("Upload & Filter")

uploaded = st.file_uploader("Upload CSV file", type=["csv"])

if uploaded:
    df = pd.read_csv(uploaded)

    st.sidebar.write(f"Rows: {df.shape[0]}, Cols: {df.shape[1]}")
    rows = st.sidebar.slider("Show rows:", 5, len(df), 10)

    tab1, tab2, tab3 = st.tabs(["Data", "Stats", "Chart"])

    with tab1:
        st.dataframe(df.head(rows))

    with tab2:
        st.write(df.describe())

    with tab3:
        num_cols = df.select_dtypes(include='number').columns.tolist()
        col = st.selectbox("Select column to plot:", num_cols)
        st.line_chart(df[col])
```

---

## 13. Quick Reference Table

| Function | Purpose |
|---|---|
| `st.title()` | App title |
| `st.write()` | Display anything |
| `st.dataframe()` | Interactive table |
| `st.text_input()` | Text input box |
| `st.slider()` | Slider widget |
| `st.selectbox()` | Dropdown |
| `st.button()` | Clickable button |
| `st.columns()` | Side-by-side layout |
| `st.sidebar` | Left sidebar |
| `st.tabs()` | Tab layout |
| `st.expander()` | Collapsible section |
| `st.line_chart()` | Quick line chart |
| `st.bar_chart()` | Quick bar chart |
| `st.pyplot()` | Matplotlib figure |
| `st.file_uploader()` | File upload |
| `st.success/error/warning()` | Alert messages |
| `st.session_state` | Persist values |

---

## Summary of Day 15
Today I learned **Streamlit** — a Python library to build interactive web apps without writing any HTML or JavaScript. I covered text elements (`title`, `header`, `write`, `markdown`, `code`), displaying DataFrames and metrics, all major **input widgets** (text input, number input, slider, selectbox, multiselect, radio, checkbox, button, date input), **layout tools** (columns, sidebar, tabs, expander), built-in **charts** (line, bar, area) and **Matplotlib integration**, **file uploader**, alert messages, and **session state** for persisting values. I also built two mini projects — a Student Grade Calculator and a CSV Data Explorer.

