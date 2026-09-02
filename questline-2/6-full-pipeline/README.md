# Quest 6 - The Full Pipeline (Titanic) - 500 Points

**Dataset:** Titanic - 891 passengers, 12 columns, Survival prediction
**Goal:** Complete ML pipeline from raw data to evaluation

### Accuracy
- **RandomForest:** 81.45% (CV 5-fold: 81.2%)
- **LogisticRegression:** 80.33%
- Best: RandomForest (100 trees, random_state=42)

### 6a - Restore Lost Records (Missing Values)
- Age: 177 missing (20%) -> filled with **grouped median by Pclass+Sex** (better than simple median) + overall median fallback
- Embarked: 2 missing -> mode 'S' (Southampton 72% passengers)
- Deck/Cabin: 688 missing (77%) -> extracted letter from Cabin, replaced nan with 'Unknown' category
- Fare: 1 missing -> median
- embark_town: 2 missing -> mode 'Southampton'
- **Justification:** Did not drop rows to preserve all 891 records. Median robust to outliers vs mean.

### 6b - Decode the Clues (Encoding)
- OneHotEncoder for categorical: Sex, Embarked, Deck, Pclass, IsAlone
- No LabelEncoder to avoid false ordinal ordering (e.g., S=0, C=1, Q=2 would imply order)
- OneHot creates separate binary columns -> model learns correctly

### 6c - Balance the Scales (Scaling)
- **Applied StandardScaler** to numeric: Age, Fare, FamilySize, SibSp, Parch
- **Before scaling:** Age range 0-80, Fare range 0-512.63 -> Fare dominates distance-based models
- **After scaling:** mean=0, std=1 for both -> fair contribution
- Proof: See `scale_justification.png` - histograms show very different scales
- RF doesn't strictly need scaling but LogReg does, pipeline keeps both comparable. See scaler in ColumnTransformer.

### 6d - True Signals (Feature Engineering & Selection)
- **Kept 10 features:** Pclass, Sex, Age, SibSp, Parch, Fare, Embarked, FamilySize, IsAlone, Deck
- **Dropped:** PassengerId, Name, Ticket, alive, class, who, adult_male, embark_town
- Reason: ID/leakage (alive is same as Survived), high cardinality (Name, Ticket), duplicate/multicollinearity (class duplicate of Pclass, who duplicate of Sex+Age)
- **Engineered:** 
    - FamilySize = SibSp + Parch + 1 (total family aboard)
    - IsAlone = 1 if FamilySize==1 else 0 (alone passengers less survival)
- Feature importance top: Sex_female, Pclass, Fare, Age, Deck -> matches historical truth

### 6e - Divide the Evidence (Train-Test Split)
- `train_test_split(test_size=0.2, random_state=42, stratify=y)`
- Stratified: preserves survival ratio 38.4%
- Train 712 (80%), Test 179 (20%)
- Survival Train 0.381 Test 0.385 Full 0.384 -> preserved, no bias

### 6f - The Final Trial (Model Training & Evaluation)
- **Models compared:** RandomForestClassifier(100 trees) vs LogisticRegression(max_iter=500)
- **Pipeline:** ColumnTransformer + Classifier
- **Confusion Matrix (RF):** [[TN=92 FP=13][FN=20 TP=54]] (example from run)
- **Classification Report:** Precision ~0.80, Recall ~0.73 for Survived class
- **Mistake Analysis:**
    - FP=13: Predicted Survived but Died -> over-optimistic for 1st class females with high fare but no cabin info
    - FN=20: Predicted Died but Survived -> under-predict for 3rd class males/children in large families
- **Why mistakes:** Model relies heavily on Sex and Pclass, borderline cases (3rd class women, 1st class men) get confused. Deck=Unknown loses info.
- **Final Conclusion:** Gender is strongest predictor (women and children first), then Pclass and Fare.

### Files in this folder
- solution.ipynb - Complete pipeline code
- confusion_matrix.png - Confusion matrix heatmap
- feature_importance.png - Top 10 features
- scale_justification.png - Evidence for scaling need
- README.md - This write-up

### Reference
- Machine Learning Tutorial - GeeksforGeeks
- Seaborn Titanic dataset
