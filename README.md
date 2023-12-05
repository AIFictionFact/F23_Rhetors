# Rhetors
AI "debates" nuanced topics scraped from r/ChangeMyView

### Outline
<sub>TLC = top-level comment   
thread = TLC + response tree</sub>
1. **Choose a topic** (fixed for demo)
2. **Evaluate & prune all threads**. Criteria:
	- A valid comment (TLC or otherwise) must have >2 upvotes (score can be 0). The top-level replies must be longer than two sentences
	- A valid thread has a depth >3
2. **Choose top 5 threads**. Best/Q&A sorting w/ favor given to threads with 1) highest !deltas awarded and 2) highest collective delta scores of posters

3. **Clean up comments**. Remove blockquotes citing other posts (keep copy), links, & other non-spoken text
4. **Assign speakers**. For each thread: speaker A is assigned the TLC.
   For each immediate reply, perform sentiment analysis or use an LLM to determine whether it agrees or disagrees with the TLC/parent comment (A).
   If it agrees, discard it and its children. If it disagrees, it is speaker B.
   Perform recursively. Some notes:
    - In later recursions, speaker may be easily determined if poster = poster two above (a reply to a reply)
   - Small cost: comparison is just the current reply against its parent

5. **Build script**:
   - Speaker C (moderator) introduces topic from post title and body. Make moderator impartial
   - The above structure is traversed depth-first. "new" speakers become A and B for each chosen thread. Speaker C introduces them
   - Use LLM to shorten any monologues, add natural transitions at the end of branches (Speaker C helps), and inject non-speech queues like [laughter] and [sighs]
   - If a reply has any children that contain blockquotes citing a part of it, introduce an interjection by that speaker
6. **TTS**. Tokenize into coherent blocks of sentences for Bark, concatenate results into one continuous dialogue


### Documentation

**Build script**:  run all the blocks in "rhetor.ipynb" in a sequential manner, installing packages as needed, and in the end, there would be a "script.json" file generated. That is the final script of the debates.

**TTS Bark**:  with the threads in "script.json", one can run the blocks in "TTS_bark.ipynb" replacing speakers names and content as need, and generate your own artificial audio debate.