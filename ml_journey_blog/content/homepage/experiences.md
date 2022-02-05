---
title: Experiences
experiences:
  - title: Data Scientist
    organization:
      name: Bottomline Technologies
      url: https://www.bottomline.com/apac
    dates: '2021 - Present'
    location: Bengaluru, India
    team: Global Data Engineering
    writeup: >

      - <b>Forecasting Payment Dates for Invoices</b>

        - Generated features and experimented with multiple regression models to get a 45% higher forecast accuracy than baseline models.

        - Implemented quantile regression to get prediction intervals to quantify confidence in predictions. Worked on creating visualizations with prediction intervals that could be interpreted by non-technical stakeholders.

      - <b>Analytics Dashboard for B2B Accounts Receivable (AR) Platform</b>
        
        - Computation and analysis of AR KPIs to develop insights on the efficiency of vendors’ AR team.
        
        - Data clustering and cluster analysis to profile and identify high-value B2B customers.

      
  - title: Trainee Decision Scientist
    organization:
      name: Mu Sigma Business Solutions
      url: https://www.mu-sigma.com/
    dates: '2019 - 2021'
    location: Bengaluru, India
    team: Innovation and Research (InD) Labs
    writeup: >

      - <b>Framework for Autonomous Adaptive Agents using Swarm Intelligence</b>

        - Literature review on proposed frameworks and architecture for adaptive systems with swarms of intelligent agents.

        - Designed and implemented an adaptive system for anomaly detection using a feedback-and-control mechanism, with Particle Swarm Optimization (Genetic Algorithm) to tune parameter weights on non-linear cost functions.

      - <b>Anomaly Detection in Financial Time Series</b>
        
        - Researched and implemented Bollinger Bands, Ornstein-Uhlenbeck and Regime-Switch models for anomaly detection on live-streamed financial security prices.
        
        - Vectorized the execution logic for offline batch-processing to achieve an 83% decrease in run-time for strategy simulation and testing.

        - Created network graph based on the correlation between asset prices and engineered network metrics to capture the evolution of the graph over time. Trained a classification model on the network metrics to detect the state of the market.

      - <b>Predictive Maintenance for Industrial IoT use-case involving Multivariate Time Series Analysis</b>

        - Explored Vector Auto-Regressive (VAR), Structured VAR and Bayesian VAR models, along with pre-processing tests (stationarity, Granger-causality and co-integration), lag optimization using information criterion and residual analysis for model diagnosis.

        - Created a configurable R Markdown file to run VAR and its variants end-to-end and generate HTML reports for any given multivariate time-series data.
      
  - title: Intern
    organization:
      name: NEC Technologies India
      url: https://in.nec.com/
    dates: 'Jan 2019 - May 2019'
    location: Noida, India
    team: Advanced Technologies and Smart Solutions (ATSS)
    writeup: >

      - <b>Natural Language Processing for CRM Automation</b>

        - Worked on creating a model to control CRM CLI with Natural Language commands.

        - Applied NLTK for text preprocessing and Stanford NLP for part-of-speech tagging and named entity recognition.

      - <b>Predictive Machine Learning for Financial Data</b>

        - Performed Exploratory Data Analysis and created a Semi-Supervised Learning (SSL) model to predict the lease absorption potential of clients

        - Implemented Self-Organizing Maps to augment the predictions of the SSL phase.

weight: 2
widget:
  handler: experiences

  # Options: sm, md, lg and xl. Default is md.
  width: 

  sidebar:
    # Options: left and right. Leave blank to hide.
    position: 
    # Options: sm, md, lg and xl. Default is md.
    scale:
  
  background:
    # Options: primary, secondary, tertiary or any valid color value. Default is primary.
    color: primary
    image:
    # Options: auto, cover and contain. Default is auto.
    size:
    # Options: center, top, right, bottom, left.
    position:
    # Options: fixed, local, scroll.
    attachment: 
---