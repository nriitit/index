<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>My Subjects</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f2f2f2;
      text-align: center;
      padding: 100px;
    }

    h1 {
      color: #333;
      margin-bottom: 50px;
    }

    .subject-button {
      padding: 15px 30px;
      font-size: 20px;
      margin: 20px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    .subject-button:hover {
      background-color: #0056b3;
    }

    /* Styling for tabs */
    .tabs {
      display: flex;
      justify-content: center;
      margin-bottom: 20px;
    }

    .tab-button {
      padding: 10px 20px;
      font-size: 16px;
      margin: 0 10px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    .tab-button:hover {
      background-color: #0056b3;
    }

    .tab-content {
      display: none;
      margin-top: 20px;
    }

    .active-tab {
      display: block;
    }
  </style>
</head>
<body>
  <h1>Welcome to My Subject Portal</h1>

  <div class="tabs">
    <button class="tab-button" onclick="showTab('bda')">BDA LAB</button>
    <button class="tab-button" onclick="showTab('ml')">ML LAB</button>
    <button class="tab-button" onclick="showTab('ml-3')">ML-3</button>
    <button class="tab-button" onclick="showTab('cns8a')">CNS8A</button>
    <button class="tab-button" onclick="showTab('cns8b')">CNS8B</button>
  </div>

  <!-- Tab Contents -->
  <div id="bda" class="tab-content">
    <button class="subject-button" onclick="window.open('https://drive.google.com/file/d/1ZLqwIfCu7R4F_RMvzbAUI0Mwc16mdwg5/preview', '_blank')">
      BDA LAB
    </button>
  </div>

  <div id="ml" class="tab-content">
    <button class="subject-button" onclick="window.open('https://drive.google.com/file/d/1YAOuKECOeBpOQeDjeZnxwybdK2dsKC3U/preview', '_blank')">
      ML LAB
    </button>
  </div>

  <div id="ml-3" class="tab-content">
    <pre>
import math
import pandas as pd
def calculate_entropy(data):
    value_counts = data.value_counts()
    total_records = len(data)
    entropy = 0
    for count in value_counts:
        prob = count / total_records
        entropy -= prob * math.log2(prob)
    return entropy

def calculate_information_gain(data, attribute, target):
    total_entropy = calculate_entropy(data[target])
    
    unique_values = data[attribute].unique()
    weighted_entropy = 0
    
    for value in unique_values:
        subset = data[data[attribute] == value]
        weighted_entropy += (len(subset) / len(data)) * calculate_entropy(subset[target])
    
    information_gain = total_entropy - weighted_entropy
    return information_gain

def id3(data, target, attributes):

    if len(data[target].unique()) == 1:
        return data[target].iloc[0]
    
    if not attributes:
        return data[target].mode()[0]
    
    info_gains = {attr: calculate_information_gain(data, attr, target) for attr in attributes}
    
    best_attribute = max(info_gains, key=info_gains.get)
    
    tree = {best_attribute: {}}
    
    for value in data[best_attribute].unique():
        subset = data[data[best_attribute] == value]
        remaining_attributes = [attr for attr in attributes if attr != best_attribute]
        subtree = id3(subset, target, remaining_attributes)
        tree[best_attribute][value] = subtree
    
    return tree

def classify(tree, sample):
    if not isinstance(tree, dict):
        return tree
    attribute = next(iter(tree))
    attribute_value = sample[attribute]
    subtree = tree[attribute].get(attribute_value)
    return classify(subtree, sample)

data = pd.DataFrame({
    'Outlook': ['Sunny', 'Sunny', 'Overcast', 'Rainy', 'Rainy', 'Rainy', 'Overcast', 'Sunny', 'Sunny', 
                'Rainy', 'Sunny', 'Overcast', 'Overcast', 'Rainy'],
    'Temperature': ['Hot', 'Hot', 'Hot', 'Mild', 'Cool', 'Cool', 'Cool', 'Mild', 'Cool', 'Mild', 'Mild', 'Mild', 
                    'Hot', 'Mild'],
    'Humidity': ['High', 'High', 'High', 'High', 'Normal', 'Normal', 'Normal', 'High', 'Normal', 'Normal', 
                 'Normal', 'High', 'Normal', 'High'],
    'Wind': ['Weak', 'Strong', 'Weak', 'Weak', 'Weak', 'Strong', 'Strong', 'Weak', 'Weak', 'Weak', 
             'Strong', 'Strong', 'Weak', 'Strong'],
    'PlayTennis': ['No', 'No', 'Yes', 'Yes', 'Yes', 'No', 'Yes', 'No', 'Yes', 'Yes', 'Yes', 'Yes', 'Yes', 'No']
})

target = 'PlayTennis'
attributes = ['Outlook', 'Temperature', 'Humidity', 'Wind']
tree = id3(data, target, attributes)

print("Decision Tree:")
print(tree)

sample = {'Outlook': 'Sunny', 'Temperature': 'Hot', 'Humidity': 'High', 'Wind': 'Weak'}
result = classify(tree, sample)
print(f"\nClassifying new sample {sample}: {result}")
    </pre>
  </div>

  <div id="cns8a" class="tab-content">
    <pre>
import java.math.BigInteger;
import java.security.SecureRandom;

public class RSA {
    public static void main(String[] args) {
        try {
            SecureRandom rand = new SecureRandom();
            BigInteger p = BigInteger.probablePrime(512, rand);
            BigInteger q = BigInteger.probablePrime(512, rand);

            BigInteger n = p.multiply(q);
            BigInteger phi = p.subtract(BigInteger.ONE).multiply(q.subtract(BigInteger.ONE));
            BigInteger e = BigInteger.valueOf(65537);
            BigInteger d = e.modInverse(phi);

            String message = "Hello, RSA!";
            BigInteger msg = new BigInteger(message.getBytes());

            BigInteger cipher = msg.modPow(e, n);
            BigInteger decrypt = cipher.modPow(d, n);
            String dec = new String(decrypt.toByteArray());

            System.out.println("Encrypted: " + cipher);
            System.out.println("Decrypted: " + dec);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
    </pre>
  </div>

  <div id="cns8b" class="tab-content">
    <pre>
#include <stdio.h>
int main()
{
    char *str = "Hello World";
    printf("Original string:%s\n", str);
    printf("After AND operation with 127:\n");
    for (int i = 0; str[i] != '\0'; i++)
    {
        char and_result = str[i] & 127;
        printf("%c", and_result);
    }

    printf("\n");
    printf("After XOR operation with 127:\n");
    for (int i = 0; str[i] != '\0'; i++)
    {
        char xor_result = str[i] ^ 127;
        printf("%c", xor_result);
    }

    printf("\n");
    return 0;
}
    </pre>
  </div>

  <script>
    function showTab(tabId) {
      // Hide all tabs
      const allTabs = document.querySelectorAll('.tab-content');
      allTabs.forEach(tab => tab.classList.remove('active-tab'));

      // Show the selected tab
      document.getElementById(tabId).classList.add('active-tab');
    }
  </script>

</body>
</html>
