# FinnovationFlows KNIME Extension
This is an Extension that provides advanced AI / LLM and in the future potential other functionality that is not yet available in the KNIME LLM / Gen AI extension.

## Included Nodes:

### Schema Generator:
The Schema Generator allows to turn an input table into a valid JSON Schema that can be passed to the Structured Output Prompter Node.
This ensures that the LLM sticks to the predefined Schema.

The node allows for the following configuration:
* Enable or disable strict mode via checkbox

the following columns need to be present in the input table:
* Fieldname(string): The name of the field in the schema.
* Datatype(string): The datatype of the field (note: Thus far only str = string is supported).
* Description(string): A description of the field.
* limitoptions(boolean): Indicates whether the field has limited options (true/false). If true, Options must be provided.
* Options(string): If the field has limited options, this column contains them separated by commas.
* isrequired(boolean): Indicates whether the field is required in the schema (true/false)

Every Row in the Input Table will be turned into one Field in the resulting JSON Schema. Please note: Thus far nesting is not supported.
Any Field will be on the first level of the resulting JSON Schema.

### Structured Output Prompter:
The Structured Output Prompter Node takes a prompt and a JSON Schema as input and generates structured output based on the provided schema. The generated output adheres to the specified schema, ensuring that it matches the expected structure and data types.

The node takes the following inputs:
* Valid JSON Schema that was created by the Schema Generator Node
* Input table that contains an arbitrary number of columns - one of the can be selected as the column that contains the user message to be provided to the LLM.

The node allows for the following configuration:
* model: manually input a valid OpenAI model - suggestion is gpt-4o or gpt-4o-mini. Exact list of available models can be found here: https://platform.openai.com/docs/models/gpt-4o-mini. Note: thus far there is no validation implemented.
* System Prompt: The system prompt to use for the OpenAI model. This System Prompt will be passed to the model for any User Message in the Input table
* User Message Column: Allows selection of the column from the input table that contains the user message.
* Credentials Parameter: Allows selection of a credentials parameter (flow variable) that was created via Credentials Widget or Credentials Configuration. The password provided in Credentials Widget or Configuration will be used as API Key


## Example Set Up in KNIME:
<img src="icons/readme/ExampleSetUp.png" width=800px/>

### Installation:

1. Download "bundle" Folder to local drive
2. Add local "bundle" Folder as Update Site: In KNIME, click Preferences (1), Install/Update (2), Available Software Sites (3), Add (4), Local (5) ==> browse to the downloaded folder and click Add (6).
<img src="icons/readme/Installation.png" width=800px/>
3. Install Extension: In KNIME, click Menu (1), Install Extensions (2), Type "AI" in Search box (3), Select "AI utilities" (4), Click next / finish until dialogue disappears
<img src="icons/readme/Installation2.png" width=800px/>
4. Wait for Installation to Finish - you will be prompted to restart KNIME
5. Search for nodes: Schema Generator and Structured Output Prompter in your node repository
<img src="icons/readme/NodeRepo.png" width=800px/>
