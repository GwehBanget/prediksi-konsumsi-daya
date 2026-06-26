# prediksi-konsumsi-daya
Aplikasi Prediksi Konsumsi Daya Listrik Menggunakan Algoritma Random Forest
import streamlit as st
import joblib
import pandas as pd

model = joblib.load("random_forest.pkl")

st.title("Prediksi Konsumsi Daya Listrik")

temperature = st.number_input("Temperature")
humidity = st.number_input("Humidity")
windspeed = st.number_input("WindSpeed")
general = st.number_input("General Diffuse Flows")
diffuse = st.number_input("Diffuse Flows")

year = st.number_input("Year", value=2017)
month = st.number_input("Month", value=1)
day = st.number_input("Day", value=1)
hour = st.number_input("Hour", value=0)
minute = st.number_input("Minute", value=0)

if st.button("Prediksi"):

    data = pd.DataFrame({
        "Temperature":[temperature],
        "Humidity":[humidity],
        "WindSpeed":[windspeed],
        "GeneralDiffuseFlows":[general],
        "DiffuseFlows":[diffuse],
        "PowerConsumption_Zone2":[0],
        "PowerConsumption_Zone3":[0],
        "Year":[year],
        "Month":[month],
        "Day":[day],
        "Hour":[hour],
        "Minute":[minute]
    })

    hasil = model.predict(data)

    st.success(f"Prediksi Konsumsi Zone 1 : {hasil[0]:.2f}")
