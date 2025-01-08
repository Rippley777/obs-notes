```
import openai
import json
import requests

# Replace with your OpenAI API key
OPENAI_API_KEY = "your_openai_api_key"

# Replace with your database API endpoint
DATABASE_API_ENDPOINT = "https://your-database-api.com/endpoint"

def call_chatgpt_api(prompt):
    """Call the ChatGPT API with a given prompt."""
    openai.api_key = OPENAI_API_KEY

    try:
        response = openai.ChatCompletion.create(
            model="gpt-3.5-turbo",
            messages=[{"role": "user", "content": prompt}],
            max_tokens=200
        )
        return response.choices[0].message["content"].strip()
    except Exception as e:
        print(f"Error calling ChatGPT API: {e}")
        return None

def save_to_json_file(data, filename):
    """Save data to a JSON file."""
    try:
        with open(filename, "w") as json_file:
            json.dump(data, json_file, indent=4)
        print(f"Data saved to {filename}")
    except Exception as e:
        print(f"Error saving to JSON file: {e}")

def send_post_request(data):
    """Send a POST request to the database API."""
    try:
        headers = {"Content-Type": "application/json"}
        response = requests.post(DATABASE_API_ENDPOINT, json=data, headers=headers)
        response.raise_for_status()
        print(f"POST request successful: {response.status_code}")
        return response.json()
    except requests.exceptions.RequestException as e:
        print(f"Error sending POST request: {e}")
        return None

def main():
    # Step 1: Call ChatGPT API
    prompt = "Generate a sample JSON object for a user profile."
    generated_data = call_chatgpt_api(prompt)

    if not generated_data:
        print("Failed to generate data from ChatGPT API.")
        return

    # Parse the generated data into a Python dictionary
    try:
        json_data = json.loads(generated_data)
    except json.JSONDecodeError as e:
        print(f"Error decoding JSON: {e}")
        return

    # Step 2: Save to a JSON file
    json_filename = "generated_data.json"
    save_to_json_file(json_data, json_filename)

    # Step 3: Send a POST request to the database
    response = send_post_request(json_data)
    if response:
        print(f"Database response: {response}")

if __name__ == "__main__":
    main()

```