from google_agents import Agent, Tool, ToolRequest, ToolResponse

# Define a custom tool
class CalculatorTool(Tool):
    def __init__(self):
        super().__init__(name="calculator", description="Performs basic arithmetic operations")

    def run(self, tool_request: ToolRequest) -> ToolResponse:
        expression = tool_request.inputs.get("expression", "")
        try:
            result = eval(expression)
            return ToolResponse(outputs={"result": str(result)})
        except Exception as e:
            return ToolResponse(outputs={"error": str(e)})

# Create the agent and register the tool
agent = Agent(tools=[CalculatorTool()])
response = agent.chat("What is 25 * 4?")
print(response.text)
