# ml
Offline training: notebooks or scripts, evaluation and exported models.
- Split train/test **by session or by time, never at random** when samples are correlated.
- Always compare against a simple rule-based baseline.
- Record for each model: data used, split, metrics, inference time on the edge container.
