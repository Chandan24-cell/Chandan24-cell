CS Engineering Student | AI & ML Specialist
Focused on building scalable AI solutions with expertise in Deep Learning, CV, and NLP. Passionate about MLOps, model optimization, and transitioning research into reliable, real-world engineering workflows....



import { useState } from "react";

const definitions = {
  "Machine Learning": "The science of teaching computers to learn from data and improve with experience — without being explicitly programmed for every task.",

  // === SUPERVISED LEARNING ===
  "1. Supervised Learning": "Training a model on labeled data — each example comes with the correct answer, so the model learns to map inputs to outputs.",
  "A. Regression": "Predicting a continuous numeric value (e.g. house price, temperature) by learning the relationship between input features and output.",
  "B. Classification": "Predicting which category an input belongs to (e.g. spam or not spam, cat or dog).",

  "Linear Regression": "Fits a straight line through data to predict a number. Simple, fast, and interpretable.",
  "Polynomial Regression": "Extends linear regression by fitting curves — useful when relationships are non-linear.",
  "Ridge Regression": "Linear regression with a penalty on large coefficients to prevent overfitting. Keeps all features but shrinks them.",
  "Lasso Regression": "Like Ridge but can shrink some coefficients to zero — effectively selecting only the most important features.",
  "ElasticNet Regression": "Combines Ridge and Lasso penalties. Best when you have many correlated features.",
  "Decision Tree Regression": "Splits data into branches based on feature values, predicting a number at each leaf.",
  "Random Forest Regression": "Builds many decision trees and averages their predictions — more accurate and stable than a single tree.",
  "Gradient Boosting Regression": "Builds trees one by one, each correcting the errors of the previous. Highly accurate.",
  "XGBoost Regression": "An optimized, fast version of gradient boosting — the go-to model for structured data competitions.",
  "LightGBM Regression": "A faster gradient boosting framework that uses a leaf-wise tree growth strategy. Great for large datasets.",
  "Support Vector Regression": "Finds a function that stays within a margin of the true values — robust to outliers.",

  "Logistic Regression": "Despite the name, it classifies. Maps inputs to a probability between 0 and 1 using a sigmoid curve.",
  "K-Nearest Neighbors": "Classifies a point by looking at its K closest neighbors and taking a majority vote.",
  "Naive Bayes": "Uses probability theory (Bayes' theorem) assuming features are independent. Fast and great for text.",
  "Decision Tree Classifier": "Splits data into branches using feature thresholds to arrive at a class prediction.",
  "Random Forest Classifier": "Ensemble of decision trees voting together — reduces overfitting, highly accurate.",
  "Support Vector Machine": "Finds the optimal boundary (hyperplane) that best separates classes with maximum margin.",
  "Gradient Boosting Classifier": "Sequentially builds trees to correct previous errors, resulting in a powerful classifier.",
  "XGBoost Classifier": "Regularized, optimized gradient boosting — fast, accurate, and widely used in production.",
  "LightGBM Classifier": "Microsoft's efficient gradient boosting framework — handles millions of rows with ease.",
  "CatBoost Classifier": "Gradient boosting that natively handles categorical features — less preprocessing needed.",
  "Neural Network Classifier": "Layers of connected nodes that learn complex patterns — the basis of deep learning.",

  // === UNSUPERVISED LEARNING ===
  "2. Unsupervised Learning": "Learning from unlabeled data — the model finds hidden patterns, structures, or groupings on its own.",
  "A. Clustering": "Grouping similar data points together without any predefined labels.",
  "B. Dimensionality Reduction": "Compressing data into fewer dimensions while preserving the most important information.",
  "C. Association Rule Learning": "Discovering interesting relationships or rules between variables in large datasets.",
  "D. Anomaly Detection": "Identifying data points that are unusual or don't fit the normal pattern.",

  "K-Means Clustering": "Partitions data into K groups by minimizing the distance from each point to its cluster center.",
  "Hierarchical Clustering": "Builds a tree of clusters — either by merging small clusters up or splitting big ones down.",
  "DBSCAN": "Groups points that are closely packed together, labeling outliers as noise. No need to specify K.",
  "Mean Shift Clustering": "Finds clusters by shifting points toward the densest region around them.",
  "Gaussian Mixture Models": "Assumes data comes from a mix of several Gaussian distributions — soft cluster assignments.",
  "Spectral Clustering": "Uses graph theory to find clusters based on connectivity rather than distance.",

  "PCA": "Principal Component Analysis — finds the directions of maximum variance to compress data while keeping structure.",
  "t-SNE": "Visualizes high-dimensional data in 2D/3D by keeping similar points close together. Great for exploration.",
  "UMAP": "Faster than t-SNE and better at preserving global structure. Popular for visualizing embeddings.",
  "LDA": "Linear Discriminant Analysis — reduces dimensions while maximizing class separability.",
  "Autoencoders": "Neural networks that compress data into a small code and reconstruct it — learn compact representations.",
  "Feature Selection": "Choosing only the most relevant features to reduce noise and improve model performance.",

  "Apriori Algorithm": "Finds frequent itemsets and association rules in transaction data (e.g. 'people who buy bread also buy butter').",
  "FP-Growth": "A faster alternative to Apriori — mines frequent patterns without candidate generation.",
  "Eclat Algorithm": "Uses vertical data format to mine frequent itemsets efficiently via set intersections.",

  "Isolation Forest": "Detects anomalies by isolating points — outliers are easier to isolate and appear in shorter branches.",
  "One-Class SVM": "Learns a boundary around normal data — anything outside is flagged as an anomaly.",
  "Local Outlier Factor": "Compares the density of a point to its neighbors — low density compared to neighbors = outlier.",
  "Autoencoder-Based Detection": "Anomalies have high reconstruction error since the model wasn't trained to reconstruct them.",
  "Statistical Outlier Detection": "Uses statistical measures like Z-score or IQR to flag points far from the distribution.",

  // === SEMI-SUPERVISED ===
  "3. Semi-Supervised Learning": "Uses a small amount of labeled data and a large amount of unlabeled data — bridges supervised and unsupervised.",
  "Self-Training": "Train on labeled data, predict on unlabeled data, add confident predictions as new labeled examples.",
  "Label Propagation": "Spreads labels from labeled to unlabeled data through a graph based on similarity.",
  "Label Spreading": "Like label propagation but smoother — allows some labeled points to change their labels too.",
  "Pseudo Labeling": "Assign predicted labels to unlabeled data and retrain the model on the combined dataset.",
  "Semi-Supervised Deep Learning": "Deep networks trained with a mix of labeled data and unlabeled data using consistency or generative techniques.",

  // === REINFORCEMENT LEARNING ===
  "4. Reinforcement Learning": "An agent learns by interacting with an environment — taking actions, receiving rewards, and maximizing long-term gain.",
  "A. Value-Based Methods": "Learn the value of being in a state or taking an action — choose the highest-value option.",
  "B. Policy-Based Methods": "Directly learn a policy (a mapping from states to actions) without a value function.",
  "C. Model-Based RL": "The agent builds an internal model of the environment to plan ahead before acting.",
  "D. Advanced RL": "Sophisticated algorithms combining value, policy, and model-based ideas for complex tasks.",

  "Q-Learning": "Learns the value of each action in each state. Tabular method — works for small state spaces.",
  "Deep Q-Network": "Q-Learning with a neural network to handle large or continuous state spaces. Played Atari at human level.",
  "Double DQN": "Reduces overestimation in DQN by using two networks — one to select actions, one to evaluate them.",

  "Policy Gradient": "Directly optimizes the policy by computing gradients of expected reward — works in continuous action spaces.",
  "REINFORCE": "A Monte Carlo policy gradient method — updates policy based on total reward of complete episodes.",
  "Actor-Critic": "Combines a policy (actor) and a value estimator (critic) — more stable than pure policy gradients.",

  "Planning-Based RL": "The agent plans by simulating future states using its environment model before acting.",
  "Environment Model Learning": "The agent learns a predictive model of the environment to simulate transitions and rewards.",

  "PPO": "Proximal Policy Optimization — clips policy updates to prevent catastrophically large changes. Widely used.",
  "A3C": "Asynchronous Advantage Actor-Critic — runs multiple agents in parallel to speed up learning.",
  "DDPG": "Deep Deterministic Policy Gradient — extends actor-critic to continuous action spaces.",
  "SAC": "Soft Actor-Critic — maximizes reward AND entropy for more robust, exploratory behavior.",
  "Multi-Agent RL": "Multiple agents learn simultaneously, cooperating or competing in a shared environment.",

  // === DEEP LEARNING ===
  "5. Deep Learning": "Machine learning using neural networks with many layers — automatically learns complex features from raw data.",
  "A. Artificial Neural Networks": "The foundation of deep learning — layers of interconnected nodes that transform inputs into outputs.",
  "B. Computer Vision Models": "Deep networks designed to understand and interpret images and videos.",
  "C. Sequence Models": "Networks designed for ordered data like text, audio, or time series.",
  "D. Generative Models": "Models that learn to generate new data resembling the training distribution.",
  "E. Transfer Learning": "Reusing knowledge from a pre-trained model to solve a new related task faster.",

  "Perceptron": "The simplest neural network — a single node that makes binary decisions. The building block of everything.",
  "Multi-Layer Perceptron": "Multiple layers of perceptrons — can learn non-linear patterns. The classic neural network.",
  "Feedforward Neural Network": "Data flows in one direction — input → hidden layers → output. No loops or memory.",

  "CNN": "Convolutional Neural Network — uses filters to detect local patterns like edges and textures in images.",
  "ResNet": "Residual Network — uses skip connections to train very deep networks without vanishing gradients.",
  "VGG": "Simple, deep CNN using only 3×3 convolutions — easy to understand and a strong baseline.",
  "Inception": "Uses parallel convolutions of different sizes to capture multi-scale features efficiently.",
  "EfficientNet": "Scales network depth, width, and resolution in a balanced way for top accuracy with fewer parameters.",
  "YOLO": "You Only Look Once — detects objects in images in a single pass. Real-time object detection.",
  "Faster R-CNN": "Region-based CNN — proposes regions then classifies them. Very accurate object detection.",
  "Vision Transformer": "Applies the Transformer architecture to image patches — rivals CNNs on many vision tasks.",

  "RNN": "Recurrent Neural Network — has memory of previous inputs. Designed for sequential data.",
  "LSTM": "Long Short-Term Memory — solves RNN's forgetting problem with gates that control information flow.",
  "GRU": "Gated Recurrent Unit — a simpler, faster alternative to LSTM with comparable performance.",
  "Transformer": "Uses self-attention to process all tokens in parallel — the architecture behind modern AI breakthroughs.",

  "Variational Autoencoders": "Encodes data into a probability distribution — enables smooth interpolation and generation of new samples.",
  "GANs": "Generative Adversarial Networks — a generator and discriminator compete, producing hyper-realistic outputs.",
  "Diffusion Models": "Learn to reverse a noising process — generate images by gradually denoising random noise. Powers DALL·E, Stable Diffusion.",
  "Large Language Models": "Massive Transformers trained on internet-scale text — can write, reason, code, and converse.",

  "Pretrained Models": "Models already trained on massive datasets — reuse their learned features instead of starting from scratch.",
  "Fine-Tuning": "Update a pretrained model's weights on your specific task — fast and effective with little data.",
  "Feature Extraction": "Freeze the pretrained model and use its outputs as features for a smaller downstream model.",
  "Foundation Models": "Enormous models (GPT, BERT, CLIP) trained broadly that can be adapted to many tasks.",

  // === NLP ===
  "6. Natural Language Processing": "Teaching machines to read, understand, and generate human language.",
  "Text Preprocessing": "Cleaning and normalizing raw text so models can process it effectively.",
  "Text Representation": "Converting text into numerical vectors that models can work with.",
  "NLP Tasks": "The core problems NLP systems are built to solve.",
  "Modern NLP": "Large-scale Transformer-based models that have revolutionized language understanding.",

  "Tokenization": "Splitting text into individual units (words, subwords, or characters) for processing.",
  "Stopword Removal": "Removing common words like 'the', 'is', 'at' that carry little meaning for many tasks.",
  "Stemming": "Reducing words to their root form by chopping off suffixes (e.g. 'running' → 'run').",
  "Lemmatization": "Reducing words to their dictionary base form using grammar rules (e.g. 'better' → 'good').",
  "Text Cleaning": "Removing HTML, special characters, extra whitespace, and other noise from raw text.",

  "Bag of Words": "Represents text as word frequency counts — simple but ignores word order and context.",
  "TF-IDF": "Weighs words by how often they appear in a document vs. how rare they are across all documents.",
  "Word2Vec": "Maps words to dense vectors where semantically similar words are geometrically close.",
  "GloVe": "Global Vectors — learns word embeddings from global word co-occurrence statistics.",
  "FastText": "Like Word2Vec but represents words as bags of character n-grams — handles unknown words well.",
  "Embeddings": "Dense vector representations that capture semantic meaning — the language of neural networks.",

  "Sentiment Analysis": "Determining the emotional tone of text — positive, negative, or neutral.",
  "Text Classification": "Assigning predefined categories to text documents (e.g. topic, language, intent).",
  "Named Entity Recognition": "Identifying and labeling entities in text — people, places, organizations, dates.",
  "Machine Translation": "Automatically translating text from one language to another (e.g. Google Translate).",
  "Question Answering": "Building systems that read text and answer questions about it.",
  "Text Summarization": "Condensing long documents into shorter versions while preserving key information.",
  "Chatbots": "Conversational agents that respond to user input using NLP techniques.",

  "Transformers": "Attention-based architecture that processes all words simultaneously — the backbone of modern NLP.",
  "BERT": "Bidirectional Encoder — reads text left-to-right AND right-to-left for deep context understanding.",
  "GPT": "Generative Pretrained Transformer — predicts the next token to generate coherent, fluent text.",
  "T5": "Text-to-Text Transfer Transformer — frames all NLP tasks as text-in, text-out problems.",
  "LLaMA": "Meta's open-source LLM family — powerful, efficient, and widely used for research and fine-tuning.",
  "Retrieval-Augmented Generation": "Combines a retriever (finds relevant documents) with a generator (produces answers) — reduces hallucination.",

  // === COMPUTER VISION ===
  "7. Computer Vision": "Enabling machines to interpret and understand visual information from the world.",
  "Image Classification": "Assigning a label to an entire image — 'is this a cat or a dog?'",
  "Object Detection": "Locating and classifying multiple objects in an image with bounding boxes.",
  "Image Segmentation": "Labeling every pixel in an image — either by object (instance) or category (semantic).",
  "Face Recognition": "Identifying or verifying a person's identity from their face.",
  "OCR": "Optical Character Recognition — extracting text from images or scanned documents.",
  "Pose Estimation": "Detecting the position of body joints to understand human posture and movement.",
  "Image Generation": "Creating new, realistic images from noise, text prompts, or other images.",
  "Video Analysis": "Understanding motion, activity, and events in video sequences over time.",

  // === TIME SERIES ===
  "8. Time Series ML": "Learning from data that changes over time — forecasting and pattern detection in sequences.",
  "Time Series Forecasting": "Predicting future values based on historical patterns (e.g. stock prices, weather).",
  "ARIMA": "AutoRegressive Integrated Moving Average — classic statistical model for time series forecasting.",
  "SARIMA": "ARIMA with seasonal components — handles repeating patterns like monthly or yearly cycles.",
  "Prophet": "Facebook's forecasting tool — handles seasonality, holidays, and missing data automatically.",
  "LSTM Forecasting": "Uses LSTM networks to capture long-range temporal dependencies for forecasting.",
  "Temporal Convolutional Networks": "Uses 1D convolutions to model sequences — often faster and more parallelizable than RNNs.",
  "Transformer Forecasting": "Applies self-attention to time series — captures complex long-range patterns.",
  "Anomaly Detection in Time Series": "Flagging unusual spikes, drops, or patterns that deviate from expected behavior.",

  // === RECOMMENDATION ===
  "9. Recommendation Systems": "Systems that suggest relevant items to users based on their preferences and behavior.",
  "Content-Based Filtering": "Recommends items similar to what a user has liked before, based on item features.",
  "Collaborative Filtering": "Recommends items liked by similar users — 'people like you also liked...'",
  "Matrix Factorization": "Decomposes the user-item interaction matrix to discover hidden preference patterns.",
  "Hybrid Recommendation": "Combines content-based and collaborative filtering for better accuracy.",
  "Neural Recommendation Systems": "Deep learning models that learn complex user-item interactions from embeddings.",
  "Ranking Models": "Learn to order items by relevance — crucial for search engines and feeds.",

  // === MODEL EVALUATION ===
  "10. Model Evaluation": "Measuring how well a model performs — essential before deploying to the real world.",
  "Classification Metrics": "Ways to measure how accurately a classifier predicts the correct category.",
  "Regression Metrics": "Ways to measure how close a regressor's predictions are to the true values.",
  "Clustering Metrics": "Ways to measure how well-defined and compact the discovered clusters are.",

  "Accuracy": "Fraction of predictions that are correct. Misleading when classes are imbalanced.",
  "Precision": "Of all predicted positives, how many are truly positive? Minimizes false alarms.",
  "Recall": "Of all true positives, how many did we catch? Minimizes missed detections.",
  "F1-Score": "Harmonic mean of Precision and Recall — balanced metric for imbalanced datasets.",
  "Confusion Matrix": "Table showing true/false positives/negatives — full picture of classification errors.",
  "ROC-AUC": "Area Under the ROC Curve — measures model's ability to distinguish between classes.",
  "Log Loss": "Penalizes confident wrong predictions — evaluates probability calibration.",

  "MAE": "Mean Absolute Error — average absolute difference between predictions and actuals. Easy to interpret.",
  "MSE": "Mean Squared Error — penalizes large errors more heavily than MAE.",
  "RMSE": "Root MSE — same units as target variable. Commonly used for intuitive interpretation.",
  "R² Score": "Proportion of variance explained by the model. 1 is perfect, 0 means no better than the mean.",
  "MAPE": "Mean Absolute Percentage Error — expresses error as a percentage of the true value.",

  "Silhouette Score": "Measures how similar a point is to its own cluster vs. other clusters. Ranges from -1 to 1.",
  "Davies-Bouldin Index": "Average similarity between clusters — lower is better, zero is perfect separation.",
  "Inertia": "Sum of squared distances from each point to its cluster center — lower means tighter clusters.",

  // === FEATURE ENGINEERING ===
  "11. Feature Engineering": "Transforming raw data into informative inputs that help models learn better.",
  "Handling Missing Values": "Strategies like imputation (filling in) or removal to deal with incomplete data.",
  "Encoding Categorical Data": "Converting non-numeric categories into numbers that models can process.",
  "Feature Scaling": "Normalizing feature ranges so no single feature dominates due to its magnitude.",

  "Label Encoding": "Assigns each category an integer. Simple but implies an artificial ordering.",
  "One-Hot Encoding": "Creates a binary column for each category — no ordering implied.",
  "Target Encoding": "Replaces category with the mean target value for that category. Powerful but needs care.",

  "Standardization": "Scales features to have zero mean and unit variance (Z-score). Works well for most algorithms.",
  "Normalization": "Scales features to a [0,1] range. Useful when you need bounded values.",
  "Robust Scaling": "Uses median and IQR — resistant to outliers unlike standardization.",

  "Feature Extraction": "Creating new features from raw data (e.g. extracting hour from a timestamp).",
  "Outlier Handling": "Identifying and treating extreme values that can distort model learning.",
  "Data Transformation": "Applying math operations (log, sqrt) to make distributions more suitable for models.",

  // === MODEL OPTIMIZATION ===
  "12. Model Optimization": "Techniques to improve model accuracy, generalization, and efficiency.",
  "Hyperparameter Tuning": "Searching for the best model configuration settings that aren't learned from data.",
  "Regularization": "Adding penalties to prevent models from memorizing training data (overfitting).",
  "Cross Validation": "Splitting data into multiple train/test folds to get a reliable performance estimate.",
  "Early Stopping": "Halt training when validation performance stops improving — avoids overfitting.",
  "Ensemble Learning": "Combining multiple models to produce better predictions than any single model.",
  "Model Compression": "Reducing model size and speed for deployment without sacrificing much accuracy.",

  "Grid Search": "Exhaustively tries every combination of hyperparameters. Thorough but slow.",
  "Random Search": "Randomly samples hyperparameter combinations — often finds good solutions faster than grid search.",
  "Bayesian Optimization": "Builds a probabilistic model of the objective to intelligently choose the next configuration.",
  "Optuna": "Modern hyperparameter framework using pruning to stop unpromising trials early.",

  "L1 Regularization": "Adds sum of absolute weights to loss — encourages sparsity by driving some weights to zero.",
  "L2 Regularization": "Adds sum of squared weights to loss — shrinks all weights smoothly, prevents large coefficients.",
  "Dropout": "Randomly disables neurons during training — forces the network to learn redundant representations.",

  "Bagging": "Trains multiple models on random data subsets and aggregates predictions. Reduces variance.",
  "Boosting": "Trains models sequentially, each focusing on previous errors. Reduces bias.",
  "Stacking": "Trains a meta-model on the predictions of base models — learns how to best combine them.",

  "Quantization": "Reduces weight precision (e.g. float32 → int8) to shrink model size and speed up inference.",
  "Pruning": "Removes unimportant weights or neurons — makes models smaller with minimal accuracy loss.",
  "Knowledge Distillation": "Trains a small 'student' model to mimic a large 'teacher' model — transfers knowledge compactly.",

  // === MLOPS ===
  "13. MLOps": "Practices and tools for deploying, monitoring, and maintaining ML models reliably in production.",
  "Data Versioning": "Tracking changes to datasets over time — like Git but for data.",
  "Experiment Tracking": "Recording hyperparameters, metrics, and results of model runs for comparison.",
  "Model Registry": "A central store for versioned, validated models — manages the model lifecycle.",
  "Model Deployment": "Serving a trained model so it can make predictions in a real application.",
  "CI/CD for ML": "Automated pipelines for testing, validating, and deploying ML code and models.",
  "Model Monitoring": "Tracking model behavior in production to detect degradation or data shifts.",
  "Automated Retraining": "Automatically retraining models when performance degrades or new data arrives.",

  "DVC": "Data Version Control — Git-like versioning for datasets and ML pipelines.",
  "MLflow": "Open-source platform for tracking experiments, packaging code, and deploying models.",
  "Weights & Biases": "Collaborative ML platform with real-time experiment tracking, visualization, and model management.",

  "Flask": "Lightweight Python web framework — simple way to wrap a model in a REST API.",
  "FastAPI": "Modern, fast Python API framework with automatic docs — preferred for ML model serving.",
  "Docker": "Packages model + dependencies into a container for consistent deployment anywhere.",
  "Kubernetes": "Orchestrates many containers at scale — auto-scaling, load balancing, self-healing deployments.",
  "Cloud Deployment": "Hosting models on AWS, GCP, or Azure for scalable, managed inference.",

  "GitHub Actions": "Automates ML workflows on code push — runs tests, trains models, deploys updates.",
  "Jenkins": "Open-source automation server for building CI/CD pipelines for ML projects.",
  "GitLab CI/CD": "Built-in CI/CD in GitLab — integrates code, testing, and deployment for ML teams.",

  "Data Drift": "When the statistical properties of input data change over time, hurting model performance.",
  "Model Drift": "When model accuracy degrades because the relationship between inputs and outputs has changed.",
  "Latency Monitoring": "Tracking how fast the model responds — critical for real-time applications.",
  "Error Monitoring": "Detecting and alerting on prediction errors, crashes, or unexpected outputs in production.",
};

const mlData = {
  name: "Machine Learning",
  color: "#00f5d4",
  children: [
    {
      name: "1. Supervised Learning", color: "#f72585",
      children: [
        { name: "A. Regression", color: "#f72585", children: ["Linear Regression","Polynomial Regression","Ridge Regression","Lasso Regression","ElasticNet Regression","Decision Tree Regression","Random Forest Regression","Gradient Boosting Regression","XGBoost Regression","LightGBM Regression","Support Vector Regression"] },
        { name: "B. Classification", color: "#f72585", children: ["Logistic Regression","K-Nearest Neighbors","Naive Bayes","Decision Tree Classifier","Random Forest Classifier","Support Vector Machine","Gradient Boosting Classifier","XGBoost Classifier","LightGBM Classifier","CatBoost Classifier","Neural Network Classifier"] }
      ]
    },
    {
      name: "2. Unsupervised Learning", color: "#7209b7",
      children: [
        { name: "A. Clustering", color: "#7209b7", children: ["K-Means Clustering","Hierarchical Clustering","DBSCAN","Mean Shift Clustering","Gaussian Mixture Models","Spectral Clustering"] },
        { name: "B. Dimensionality Reduction", color: "#7209b7", children: ["PCA","t-SNE","UMAP","LDA","Autoencoders","Feature Selection"] },
        { name: "C. Association Rule Learning", color: "#7209b7", children: ["Apriori Algorithm","FP-Growth","Eclat Algorithm"] },
        { name: "D. Anomaly Detection", color: "#7209b7", children: ["Isolation Forest","One-Class SVM","Local Outlier Factor","Autoencoder-Based Detection","Statistical Outlier Detection"] }
      ]
    },
    {
      name: "3. Semi-Supervised Learning", color: "#4cc9f0",
      children: ["Self-Training","Label Propagation","Label Spreading","Pseudo Labeling","Semi-Supervised Deep Learning"]
    },
    {
      name: "4. Reinforcement Learning", color: "#f77f00",
      children: [
        { name: "A. Value-Based Methods", color: "#f77f00", children: ["Q-Learning","Deep Q-Network","Double DQN"] },
        { name: "B. Policy-Based Methods", color: "#f77f00", children: ["Policy Gradient","REINFORCE","Actor-Critic"] },
        { name: "C. Model-Based RL", color: "#f77f00", children: ["Planning-Based RL","Environment Model Learning"] },
        { name: "D. Advanced RL", color: "#f77f00", children: ["PPO","A3C","DDPG","SAC","Multi-Agent RL"] }
      ]
    },
    {
      name: "5. Deep Learning", color: "#06d6a0",
      children: [
        { name: "A. Artificial Neural Networks", color: "#06d6a0", children: ["Perceptron","Multi-Layer Perceptron","Feedforward Neural Network"] },
        { name: "B. Computer Vision Models", color: "#06d6a0", children: ["CNN","ResNet","VGG","Inception","EfficientNet","YOLO","Faster R-CNN","Vision Transformer"] },
        { name: "C. Sequence Models", color: "#06d6a0", children: ["RNN","LSTM","GRU","Transformer"] },
        { name: "D. Generative Models", color: "#06d6a0", children: ["Autoencoders","Variational Autoencoders","GANs","Diffusion Models","Large Language Models"] },
        { name: "E. Transfer Learning", color: "#06d6a0", children: ["Pretrained Models","Fine-Tuning","Feature Extraction","Foundation Models"] }
      ]
    },
    {
      name: "6. Natural Language Processing", color: "#ffd166",
      children: [
        { name: "Text Preprocessing", color: "#ffd166", children: ["Tokenization","Stopword Removal","Stemming","Lemmatization","Text Cleaning"] },
        { name: "Text Representation", color: "#ffd166", children: ["Bag of Words","TF-IDF","Word2Vec","GloVe","FastText","Embeddings"] },
        { name: "NLP Tasks", color: "#ffd166", children: ["Sentiment Analysis","Text Classification","Named Entity Recognition","Machine Translation","Question Answering","Text Summarization","Chatbots"] },
        { name: "Modern NLP", color: "#ffd166", children: ["Transformers","BERT","GPT","T5","LLaMA","Retrieval-Augmented Generation"] }
      ]
    },
    {
      name: "7. Computer Vision", color: "#ef476f",
      children: ["Image Classification","Object Detection","Image Segmentation","Face Recognition","OCR","Pose Estimation","Image Generation","Video Analysis"]
    },
    {
      name: "8. Time Series ML", color: "#118ab2",
      children: ["Time Series Forecasting","ARIMA","SARIMA","Prophet","LSTM Forecasting","Temporal Convolutional Networks","Transformer Forecasting","Anomaly Detection in Time Series"]
    },
    {
      name: "9. Recommendation Systems", color: "#9d4edd",
      children: ["Content-Based Filtering","Collaborative Filtering","Matrix Factorization","Hybrid Recommendation","Neural Recommendation Systems","Ranking Models"]
    },
    {
      name: "10. Model Evaluation", color: "#43aa8b",
      children: [
        { name: "Classification Metrics", color: "#43aa8b", children: ["Accuracy","Precision","Recall","F1-Score","Confusion Matrix","ROC-AUC","Log Loss"] },
        { name: "Regression Metrics", color: "#43aa8b", children: ["MAE","MSE","RMSE","R² Score","MAPE"] },
        { name: "Clustering Metrics", color: "#43aa8b", children: ["Silhouette Score","Davies-Bouldin Index","Inertia"] }
      ]
    },
    {
      name: "11. Feature Engineering", color: "#ff6b6b",
      children: [
        "Handling Missing Values",
        { name: "Encoding Categorical Data", color: "#ff6b6b", children: ["Label Encoding","One-Hot Encoding","Target Encoding"] },
        { name: "Feature Scaling", color: "#ff6b6b", children: ["Standardization","Normalization","Robust Scaling"] },
        "Feature Selection","Feature Extraction","Outlier Handling","Data Transformation"
      ]
    },
    {
      name: "12. Model Optimization", color: "#48cae4",
      children: [
        { name: "Hyperparameter Tuning", color: "#48cae4", children: ["Grid Search","Random Search","Bayesian Optimization","Optuna"] },
        { name: "Regularization", color: "#48cae4", children: ["L1 Regularization","L2 Regularization","Dropout"] },
        "Cross Validation","Early Stopping",
        { name: "Ensemble Learning", color: "#48cae4", children: ["Bagging","Boosting","Stacking"] },
        { name: "Model Compression", color: "#48cae4", children: ["Quantization","Pruning","Knowledge Distillation"] }
      ]
    },
    {
      name: "13. MLOps", color: "#a8dadc",
      children: [
        { name: "Data Versioning", color: "#a8dadc", children: ["DVC"] },
        { name: "Experiment Tracking", color: "#a8dadc", children: ["MLflow","Weights & Biases"] },
        "Model Registry",
        { name: "Model Deployment", color: "#a8dadc", children: ["Flask","FastAPI","Docker","Kubernetes","Cloud Deployment"] },
        { name: "CI/CD for ML", color: "#a8dadc", children: ["GitHub Actions","Jenkins","GitLab CI/CD"] },
        { name: "Model Monitoring", color: "#a8dadc", children: ["Data Drift","Model Drift","Latency Monitoring","Error Monitoring"] },
        "Automated Retraining"
      ]
    }
  ]
};

function Tooltip({ name, color }) {
  const def = definitions[name];
  if (!def) return null;
  return (
    <div style={{
      position: "absolute",
      left: "calc(100% + 12px)",
      top: "50%",
      transform: "translateY(-50%)",
      zIndex: 1000,
      background: "#12121f",
      border: `1px solid ${color}50`,
      borderLeft: `3px solid ${color}`,
      borderRadius: 8,
      padding: "10px 14px",
      width: 280,
      boxShadow: `0 8px 32px #00000080, 0 0 0 1px ${color}15`,
      pointerEvents: "none",
    }}>
      <div style={{ fontSize: 11, fontWeight: 700, color: color, marginBottom: 5, fontFamily: "'Space Mono', monospace" }}>
        {name}
      </div>
      <div style={{ fontSize: 11, color: "#bbb", lineHeight: 1.6, fontFamily: "'JetBrains Mono', monospace" }}>
        {def}
      </div>
    </div>
  );
}

function LeafNode({ name, color }) {
  const [hovered, setHovered] = useState(false);
  const def = definitions[name];
  return (
    <div
      style={{ position: "relative", display: "inline-block", margin: "2px" }}
      onMouseEnter={() => setHovered(true)}
      onMouseLeave={() => setHovered(false)}
    >
      <div style={{
        display: "inline-flex",
        alignItems: "center",
        gap: 6,
        background: hovered ? `${color}28` : `${color}12`,
        border: `1px solid ${color}${hovered ? "70" : "35"}`,
        borderRadius: 20,
        padding: "4px 10px",
        fontSize: 11,
        color: hovered ? "#fff" : "#bbb",
        fontFamily: "'JetBrains Mono', monospace",
        cursor: def ? "help" : "default",
        transition: "all 0.15s",
        whiteSpace: "nowrap",
      }}>
        <span style={{ width: 5, height: 5, borderRadius: "50%", background: color, flexShrink: 0 }} />
        {name}
        {def && <span style={{ fontSize: 8, color: `${color}90`, marginLeft: 2 }}>?</span>}
      </div>
      {hovered && def && <Tooltip name={name} color={color} />}
    </div>
  );
}

function DefinitionPanel({ name, color, onClose }) {
  const def = definitions[name];
  if (!def) return null;
  return (
    <div style={{
      background: "#0d0d1a",
      border: `1px solid ${color}40`,
      borderLeft: `4px solid ${color}`,
      borderRadius: 10,
      padding: "12px 16px",
      margin: "6px 0 8px 0",
      maxWidth: 520,
    }}>
      <div style={{ fontSize: 10, color: `${color}cc`, fontWeight: 700, marginBottom: 4, fontFamily: "'Space Mono', monospace", letterSpacing: "0.5px" }}>
        DEFINITION
      </div>
      <div style={{ fontSize: 12, color: "#ccc", lineHeight: 1.7, fontFamily: "'JetBrains Mono', monospace" }}>
        {def}
      </div>
    </div>
  );
}

function TreeNode({ node, depth = 0, parentColor }) {
  const [open, setOpen] = useState(depth < 1);
  const [showDef, setShowDef] = useState(false);

  if (typeof node === "string") {
    return <LeafNode name={node} color={parentColor || "#00f5d4"} />;
  }

  const color = node.color || parentColor || "#00f5d4";
  const isRoot = depth === 0;
  const hasDef = !!definitions[node.name];
  const allLeaves = node.children && node.children.every(c => typeof c === "string");

  return (
    <div style={{ marginLeft: depth === 0 ? 0 : 16, position: "relative" }}>
      {!isRoot && (
        <div style={{
          position: "absolute", left: -12, top: 0, bottom: 0,
          width: 1, background: `${color}25`,
        }} />
      )}

      <div style={{ display: "flex", alignItems: "center", gap: 6, flexWrap: "wrap" }}>
        <button
          onClick={() => !isRoot && setOpen(o => !o)}
          style={{
            display: "flex",
            alignItems: "center",
            gap: 8,
            background: isRoot
              ? `linear-gradient(135deg, ${color}22, ${color}10)`
              : open ? `${color}18` : `${color}08`,
            border: `1px solid ${color}${isRoot ? "80" : "30"}`,
            borderRadius: isRoot ? 12 : 8,
            padding: isRoot ? "10px 20px" : depth === 1 ? "6px 14px" : "4px 12px",
            cursor: isRoot ? "default" : "pointer",
            color: isRoot ? color : open ? "#fff" : "#ccc",
            fontSize: isRoot ? 20 : depth === 1 ? 13 : 12,
            fontFamily: isRoot ? "'Space Mono', monospace" : "'JetBrains Mono', monospace",
            fontWeight: isRoot ? 700 : depth === 1 ? 600 : 500,
            marginBottom: 3,
            marginTop: isRoot ? 0 : 2,
            textAlign: "left",
            transition: "all 0.2s",
            boxShadow: isRoot ? `0 0 24px ${color}20` : "none",
          }}
        >
          {!isRoot && (
            <span style={{
              display: "inline-block", width: 15, height: 15, borderRadius: 3,
              background: `${color}25`, border: `1px solid ${color}55`,
              fontSize: 9, color: color, textAlign: "center",
              lineHeight: "14px", fontWeight: 700, flexShrink: 0,
            }}>
              {open ? "−" : "+"}
            </span>
          )}
          {isRoot && <span style={{ fontSize: 22 }}>🧠</span>}
          <span>{node.name}</span>
          {!isRoot && node.children && (
            <span style={{
              fontSize: 9, color: `${color}70`, background: `${color}18`,
              borderRadius: 10, padding: "1px 6px",
            }}>
              {node.children.length}
            </span>
          )}
        </button>

        {hasDef && !isRoot && (
          <button
            onClick={() => setShowDef(s => !s)}
            title="Show definition"
            style={{
              background: showDef ? `${color}30` : `${color}10`,
              border: `1px solid ${color}${showDef ? "60" : "30"}`,
              borderRadius: 20,
              padding: "2px 9px",
              cursor: "pointer",
              color: showDef ? color : `${color}80`,
              fontSize: 10,
              fontFamily: "'JetBrains Mono', monospace",
              transition: "all 0.15s",
            }}
          >
            {showDef ? "▲ hide" : "▼ what's this?"}
          </button>
        )}
      </div>

      {showDef && hasDef && !isRoot && (
        <div style={{ marginLeft: 4 }}>
          <DefinitionPanel name={node.name} color={color} />
        </div>
      )}

      {(isRoot || open) && node.children && (
        <div style={{
          marginLeft: isRoot ? 0 : 14,
          paddingLeft: isRoot ? 0 : 8,
          borderLeft: isRoot ? "none" : `1px solid ${color}18`,
          marginTop: 2, marginBottom: isRoot ? 0 : 4,
        }}>
          {allLeaves ? (
            <div style={{ display: "flex", flexWrap: "wrap", gap: 2, padding: "4px 0" }}>
              {node.children.map((c, i) => (
                <LeafNode key={i} name={c} color={color} />
              ))}
            </div>
          ) : (
            node.children.map((child, i) => (
              <TreeNode key={i} node={child} depth={depth + 1} parentColor={color} />
            ))
          )}
        </div>
      )}
    </div>
  );
}

export default function MLTree() {
  const [search, setSearch] = useState("");

  const countAll = (() => {
    let n = 0;
    const walk = (node) => {
      if (typeof node === "string") { n++; return; }
      if (node.children) node.children.forEach(walk);
    };
    mlData.children.forEach(walk);
    return n;
  })();

  return (
    <div style={{
      minHeight: "100vh",
      background: "#080810",
      color: "#e0e0e0",
      fontFamily: "'JetBrains Mono', monospace",
      padding: "32px 24px",
      backgroundImage: `
        radial-gradient(ellipse at 15% 15%, #00f5d418 0%, transparent 45%),
        radial-gradient(ellipse at 85% 85%, #7209b718 0%, transparent 45%)
      `,
    }}>
      <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600;700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet" />

      <div style={{ maxWidth: 860, margin: "0 auto 28px" }}>
        <h1 style={{
          margin: "0 0 4px",
          fontSize: 26,
          fontFamily: "'Space Mono', monospace",
          fontWeight: 700,
          background: "linear-gradient(135deg, #00f5d4, #7209b7)",
          WebkitBackgroundClip: "text",
          WebkitTextFillColor: "transparent",
        }}>
          ML Knowledge Tree
        </h1>
        <p style={{ margin: "0 0 16px", fontSize: 11, color: "#555" }}>
          13 domains · {countAll} topics · hover leaf nodes or click <span style={{ color: "#00f5d480" }}>▼ what's this?</span> for definitions
        </p>

        <div style={{ display: "flex", flexWrap: "wrap", gap: 6 }}>
          {mlData.children.map((cat, i) => (
            <div key={i} style={{ display: "flex", alignItems: "center", gap: 4, fontSize: 10, color: "#666" }}>
              <span style={{ width: 8, height: 8, borderRadius: 2, background: cat.color, flexShrink: 0 }} />
              {cat.name.replace(/^\d+\.\s/, "")}
            </div>
          ))}
        </div>
      </div>

      <div style={{
        maxWidth: 860, margin: "0 auto",
        background: "#ffffff03",
        border: "1px solid #ffffff08",
        borderRadius: 16,
        padding: "24px",
      }}>
        <TreeNode node={mlData} depth={0} />
      </div>

      <p style={{ textAlign: "center", fontSize: 10, color: "#2a2a3a", marginTop: 20 }}>
        Machine Learning · Complete Reference Tree
      </p>
    </div>
  );
}
