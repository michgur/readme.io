# SDK input format- python SDK v0.6, node SDK v0.3
*these version maintain backwards compatibilty with old SDK code*

### top snippet = python, bottom snippet = node

--------------
* document input- pass as a string

```python
pipline.run('hello')
```
```node
await pipeline.run('hello');
```
* conversation input- pass as a list of Utterance object

```python
conversation = [
  oneai.Utterance('michael', 'hello'),
  ...
]
pipline.run(conversation)
```
```node
const conversation = [
  { speaker: 'michael', utterance: 'hi' },
  ...
]
await pipeline.run(conversation);
```
* file input - sync
```python
import asyncio

# binary file
with open('myfile.mp3', 'rb') as inputf:
  output = pipline.run(inputf)
  
# text file
with open('myotherfile.txt', 'r') as inputf:
  output = pipline.run(inputf)
```
```node
await pipeline.runFile('myfile.mp3', { sync: true });
```
* file input - async
```python
import asyncio

async def main():
  with open('myfile.mp3', 'rb') as inputf:
    output = await pipline.run(inputf, timeout)

asyncio.run(main())
```
```node
await pipeline.runFile('myfile.mp3');
```
* batch processing
```python
pipeline.run_batch(
  ['a', 'b', 'c', ...],
  on_output=lambda input, output: print(input, output.summary.text)
)
```
```node
await pipeline.runBatch(
  ['a', 'b', 'c', ...],
  {onOutput: (input, output) => {console.log(`${input} ${output.summary.text}`)} }
)
```
