import streamlit as st
import pandas as pd
import numpy as np
import plotly.graph_objects as go
import time

# 1. Page Configuration for a High-Tech Dashboard
st.set_page_config(page_title="Aegis-Drive V1.0", layout="wide", initial_sidebar_state="collapsed")

# Inject a custom title block using your HTML skill
st.markdown("""
    <div style='background-color:#0d1117; padding:15px; border-radius:10px; border: 1px solid #238636; text-align:center;'>
        <h1 style='color:#238636; margin:0;'>AEGIS-DRIVE // AUTONOMOUS EDGE INTERACTION MATRIX</h1>
        <p style='color:#8b949e; margin:5px 0 0 0;'>Lead Architect Portfolio Project - Darshi Dholakia</p>
    </div>
""", unsafe_allow_html=True)

st.write("") # Spacer

# 2. Main Layout Split (Left: Driving Feed | Right: System Telemetry)
col1, col2 = st.columns([3, 2])

with col1:
    st.subheader("🌐 Real-Time In-Car Vehicle Perception Feed")
    # Replace this URL with any YouTube link or local path of a dashcam driving video
    video_url = "https://youtube.com" 
    st.video(video_url)
    
    st.caption("AI Edge Processing Loop actively checking frames at 30 FPS for structural anomalies.")

with col2:
    st.subheader("📊 System Architecture Telemetry")
    
    # Simulation Controller Button for the Interview
    st.info("💡 Pro-Tip for Panel: Click below to simulate the 60-second real-time fleet run.")
    if st.button("🚀 Execute Fleet Architecture Simulation", use_container_width=True):
        
        # Placeholders to update data dynamically in the loop
        status_box = st.empty()
        metric_col1, metric_col2 = st.columns(2)
        m1 = metric_col1.empty()
        m2 = metric_col2.empty()
        chart_placeholder = st.empty()
        
        cost_saved_data = []
        timestamps = []
        cumulative_savings = 0
        
        # Simulated 20-step loop representing vehicle timeline
        for t in range(1, 21):
            timestamps.append(t)
            
            # --- THE SCENARIO LOGIC ---
            # Steps 1 to 11: Normal highway driving. Data is filtered out locally.
            if t < 12:
                status_box.markdown("""
                    <div style='background-color:#161b22; padding:12px; border-radius:5px; border-left: 5px solid #238636;'>
                        <strong style='color:#238636;'>STATUS: PASSIVE FILTERING ACTIVE</strong><br>
                        <span style='color:#c9d1d9; font-size:14px;'>Scenario nominal. Road clear. Discarding repetitive video frames at edge.</span>
                    </div>
                """, unsafe_allow_html=True)
                
                speed = int(80 + np.random.randint(-3, 4))
                bandwidth = "0.0 Kbps (Block)"
                savings_increment = 35  # Rupees saved per step
                cumulative_savings += savings_increment
                
            # Steps 12 to 15: The Anomaly hits (Car cuts in / Pedestrian stepping out)
            elif 12 <= t <= 15:
                status_box.markdown("""
                    <div style='background-color:#210e12; padding:12px; border-radius:5px; border-left: 5px solid #f85149; animation: blink 1s infinite;'>
                        <strong style='color:#f85149;'>⚠️ ALERT: CRITICAL DRIVING ANOMALY ENCOUNTERED</strong><br>
                        <span style='color:#c9d1d9; font-size:14px;'>Confidence Score < 95%. Overriding Edge Filter. Uploading 10s RAW data chunk to AWS Cloud.</span>
                    </div>
                """, unsafe_allow_html=True)
                
                speed = int(45 - (t - 11) * 8) # Vehicle actively braking hard
                bandwidth = "12.4 Mbps (Uplink)"
                savings_increment = 0 # Uploading costs money, no savings here
                cumulative_savings += savings_increment
                
            # Steps 16 to 20: Recovery phase after the car safely handles the obstacle
            else:
                status_box.markdown("""
                    <div style='background-color:#161b22; padding:12px; border-radius:5px; border-left: 5px solid #1f6feb;'>
                        <strong style='color:#1f6feb;'>STATUS: SCENARIO RESOLVED // RESUMING STACK</strong><br>
                        <span style='color:#c9d1d9; font-size:14px;'>Threat cleared. Resuming local loop execution. Re-engaging data filters.</span>
                    </div>
                """, unsafe_allow_html=True)
                
                speed = int(60 + (t - 15) * 4)
                bandwidth = "0.0 Kbps (Block)"
                savings_increment = 35
                cumulative_savings += savings_increment

            cost_saved_data.append(cumulative_savings)
            
            # Update Live Value Cards
            m1.metric(label="🏎️ Current Vehicle Speed", value=f"{speed} km/h")
            m2.metric(label="📡 Cellular Upload Pipeline", value=bandwidth)
            
            # Update the Live Line Chart using Plotly
            fig = go.Figure()
            fig.add_trace(go.Scatter(
                x=timestamps, 
                y=cost_saved_data, 
                mode='lines+markers',
                name='Infrastructure ROI',
                line=dict(color='#238636' if t < 12 else '#f85149', width=3)
            ))
            fig.update_layout(
                title=f"Cumulative Cloud Storage Costs Saved: ₹{cumulative_savings}",
                xaxis_title="Simulation Time Steps",
                yaxis_title="Savings (INR)",
                template="plotly_dark",
                margin=dict(l=20, r=20, t=40, b=20),
                height=250
            )
            chart_placeholder.plotly_chart(fig, use_container_width=True)
            
            time.sleep(0.6) # Controls speed of data ticking on screen during interview
