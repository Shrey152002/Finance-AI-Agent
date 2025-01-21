# Finance Agent Using Phidata Tools

This project demonstrates the creation and usage of a finance-focused agent powered by the Phidata framework. The agent leverages the Groq model, YFinance tools, and custom utilities to analyze and compare financial data, including stock prices, analyst recommendations, and company fundamentals.

## Features

### 1. **Agent Overview**

The agent is built using the `phi.agent.Agent` class and is equipped with:

- **Model**: A Groq model (`llama-3.3-70b-versatile`) for versatile natural language processing tasks.
- **Tools**: YFinance tools for fetching real-time stock-related data and a custom tool for resolving company symbols.
- **Instructions**: Guidelines for displaying data in tabular format and utilizing tools effectively.

### 2. **Functionalities**

- Fetch stock prices, analyst recommendations, and fundamentals for specified companies.
- Compare data for multiple companies.
- Display results in a user-friendly table format.

## Setup Instructions

### Prerequisites

Ensure you have the following installed:

- Python 3.9+
- `phi` library (Phidata framework)
- `dotenv` for environment variable management
- API keys for financial data access if required by YFinanceTools

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/your-repo/finance-agent.git
   cd finance-agent
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Set up environment variables:

   - Create a `.env` file in the project directory.
   - Add any required API keys or configuration variables for your tools.

4. Run the script:

   ```bash
   python main.py
   ```

## Code Explanation

### Custom Function: `get_company_symbol`

This function resolves a company name to its stock symbol. It supports popular companies like Tesla (`TSLA`), Microsoft (`MSFT`), and more. If the company is not recognized, it returns "Unknown."

```python
def get_company_symbol(company: str) -> str:
    symbols = {
        "Phidata": "MSFT",
        "Infosys": "INFY",
        "Tesla": "TSLA",
        "Apple": "AAPL",
        "Microsoft": "MSFT",
        "Amazon": "AMZN",
        "Google": "GOOGL",
    }
    return symbols.get(company, "Unknown")
```

### Agent Configuration

The agent is configured with:

- A Groq model (`llama-3.3-70b-versatile`) for advanced text processing.
- YFinance tools to fetch and process financial data.
- Custom instructions to guide its operations, ensuring outputs are well-structured and informative.

```python
agent = Agent(
    model=Groq(id="llama-3.3-70b-versatile"),
    tools=[
        YFinanceTools(
            stock_price=True,
            analyst_recommendations=True,
            stock_fundamentals=True
        ),
        get_company_symbol
    ],
    instructions=[
        "Use tables to display data.",
        "If you need to find the symbol for a company, use the get_company_symbol tool.",
    ],
    show_tool_calls=True,
    markdown=True,
    debug_mode=True,
)
```

### Running the Agent

The `agent.print_response` function executes the query, fetching and comparing data for Tesla (`TSLA`) and Phidata. Results are displayed in a tabular format for clarity.

```python
agent.print_response(
    "Summarize and compare analyst recommendations and fundamentals for TSLA and Phidata. Show in tables.",
    stream=True
)
```

## Example Output

The agent processes the query and generates a response in Markdown with tables, such as:

| Metric         | Tesla (TSLA) | Phidata (MSFT)     |
| -------------- | ------------ | ------------------ |
| Analyst Rating | Buy (4.5/5)  | Strong Buy (4.8/5) |
| Current Price  | \$720        | \$320              |
| Market Cap     | \$700B       | \$2T               |

## Customization

You can expand this project by:

- Adding more tools for advanced financial data analysis.
- Extending `get_company_symbol` with a database or API integration for dynamic symbol lookup.
- Integrating visualization libraries (e.g., Matplotlib or Plotly) for graphical insights.

## License

This project is licensed under the MIT License.



