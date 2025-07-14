# brainimport streamlit as st
import google.generativeai as genai

# Your Gemini API Key
genai.configure(api_key="AIzaSyCQYZDUws4GzHOqop6-FC7UlMS4jXc3P-U")  # <-- yahan apni API key daalo

model = genai.GenerativeModel('gemini-pro')

st.set_page_config(page_title="Mental Health Companion", page_icon="🧠")
st.title("🧠 Mental Health Companion")
st.write("A supportive AI that listens and helps you feel better.")

user_input = st.text_area("How are you feeling today?", height=150)

if st.button("Get Support"):
    if user_input.strip() == "":
        st.warning("Please share how you're feeling.")
    else:
        prompt = f"""
You are a kind, supportive, and empathetic mental health companion. Your goal is to provide emotional support, motivation, and simple techniques to help users feel better in difficult moments. 

Always respond in a calm, non-judgmental, and positive tone. Keep answers short, encouraging, and practical. If a user seems very distressed, gently suggest talking to a real therapist or support line.

Now, the user says: "{user_input}"
"""
        response = model.generate_content(prompt)
        st.markdown("### 🌟 Response")
        st.write(response.text)
