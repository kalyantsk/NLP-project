Instructions : - 

1. Install Dependencies
Ensure you have Python 3.x installed. Then, install the required libraries using the following command:
bash
Copy code
pip install gensim
2. Load Pre-trained Models
The project uses FastText and Word2Vec models from Gensim’s API. Load the models as shown below:
python
Copy code
import gensim.downloader as api

# Load FastText and Word2Vec models
fasttext_model = api.load('fasttext-wiki-news-subwords-300')
word2vec_model = api.load('word2vec-google-news-300')
3. Find Word Analogies
To find word analogies, use the find_analogies() function. Provide three words in the analogy form "A : B :: C : ?":
python
Copy code
def find_analogies(model, word_a, word_b, word_c):
    result = model.most_similar(positive=[word_b, word_c], negative=[word_a], topn=1)
    return result[0][0]
Example:
python
Copy code
result = find_analogies(fasttext_model, 'king', 'man', 'woman')
print(result)  # Output: 'queen'
4. Interactive Testing
You can test the word analogy function interactively by running:
python
Copy code
def interactive_testing():
    while True:
        word_a = input("Enter word A (or 'exit' to quit): ")
        if word_a.lower() == 'exit':
            break
        word_b = input("Enter word B: ")
        word_c = input("Enter word C: ")

        result_ft = find_analogies(fasttext_model, word_a, word_b, word_c)
        print(f"FastText result: {result_ft}")

        result_w2v = find_analogies(word2vec_model, word_a, word_b, word_c)
        print(f"Word2Vec result: {result_w2v}")
This allows users to input any word analogy and get predictions in real-time.

