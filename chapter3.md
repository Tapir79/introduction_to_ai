# Summary: Reasoning Under Uncertainty (Simple Explanation)

## 1. Why We Need to Handle Uncertainty
AI often deals with incomplete or unclear information. Many approaches exist (fuzzy logic, plausible reasoning, etc.), but **probability theory** is the most consistent and reliable method for handling uncertainty.

The text also mentions a humorous argument from a fuzzy logic supporter who rejected a proof in favor of probability theory simply because the proof used ordinary logic.

---

## 2. Basics of Probability (Key Concepts)
To use probability in AI, we need some basic ideas:

- **Probabilistic model** – Describes how random variables relate to each other.
- **Events** – Things that may or may not happen.
- **Joint probability** – Probability that multiple events happen together.
- **Conditional probability** – Probability of one event given another.

Suggested references:
- *Deep Learning* (Goodfellow, Bengio, Courville)
- *All of Statistics* (Wasserman)

---

## 3. Bayes’ Rule
**Bayes’ rule** lets us update our beliefs when we see new data.

Formula:

`P(state | observation) = P(state) * P(observation | state) / P(observation)`

Where:

- **Posterior**: `P(state | observation)`  
  → Updated probability after seeing the observation  
- **Prior**: `P(state)`  
  → Probability before seeing the observation  
- **Likelihood**: `P(observation | state)`  
  → How likely the observation is given the state  
- **Evidence** (the “annoying denominator”): `P(observation)`  
  → Normalizes the probabilities; often hard to compute

Bayes’ rule is central to modern AI and machine learning.

---

## 4. Probabilistic Inference
**Probabilistic inference** means using probability to figure out unknown things (states) based on what we observe.

Examples:
- Inferring a disease from symptoms  
- Detecting spam emails  
- Estimating hidden causes from visible effects  

---

## 5. Avoiding the “Annoying Denominator”
The denominator `P(observation)` can be difficult to compute.  
A useful trick is to compute **ratios** of posterior probabilities instead:

`R = P(State=1 | obs) / P(State=2 | obs)`

Applying Bayes’ rule to both terms:

`R = [P(State=1) * P(obs | State=1)] / [P(State=2) * P(obs | State=2)]`

Notice that `P(obs)` cancels out — we never have to compute it.

If State 1 and State 2 are the only possibilities, then:

`P(State=2 | obs) = 1 - P(State=1 | obs)`

And from the ratio, we can get the actual probability:

`P(State=1 | obs) = R / (1 + R)`

This allows inference without ever computing the denominator directly.

---

## 6. Key Takeaways
- Probability theory is the most principled method for handling uncertainty in AI.  
- Bayes’ rule is the main tool for updating beliefs based on evidence.  
- Using ratios avoids computing the difficult denominator.  
- These ideas form the foundation of many AI and machine learning techniques.


# Summary: Naive Bayes Classification (Simple Explanation)

## 1. What Naive Bayes Is
The **naive Bayes classifier** is a machine learning method that uses **Bayes’ rule** to classify objects (such as emails, documents, or images) into different categories.  
It learns from training data where the correct class labels are already known.

---

## 2. How the Model Works
Naive Bayes is a **probabilistic model** with:

- **One class variable**  
  → The category we want to predict (e.g., spam or not spam)

- **Many feature variables**  
  → Pieces of information describing the object  
    (in email filtering, these are the words in the message)

### The key assumption:
`The feature variables are conditionally independent given the class.`  
This means that once we know the class (spam or not spam), the features (words) are treated as if they don’t influence each other.

This assumption is often unrealistic in the real world — but surprisingly, the classifier still works very well.

---

## 3. Example: Spam Filtering
In a spam filter:

- The **class variable** = “spam” or “ham” (legitimate email).  
- The **features** = the words in the email.  
  Each word is treated as a separate feature variable.

The number of feature variables therefore depends on how many words the email contains.

---

## 4. Representation as a Bayesian Network
The naive Bayes model can be drawn as a **Bayesian network**, where:

- The **class variable** sits at the top.
- Each **feature variable** (word) depends directly on the class.
- Feature variables do **not** depend on each other (because of the independence assumption).

This structure visually encodes the “naive” independence assumption.  
The course will return to Bayesian networks later.

---

## 5. Key Takeaways
- Naive Bayes uses Bayes’ rule to classify data.
- It assumes features are independent given the class (the “naive” assumption).
- Despite being simple and often unrealistic, it works extremely well in practice.
- It is widely used for tasks like **spam detection**, **text classification**, and **document filtering**.
