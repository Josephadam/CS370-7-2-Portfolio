# CS370-7-2-Portfolio
<h2>Project Overview</h2>
<p>
  This project focuses on training an intelligent agent to navigate a maze environment using reinforcement learning.
  The goal was to enable the agent to find the treasure through exploration and learning from previous experiences.
  The foundation of this project included prewritten files such as <code>TreasureMaze.py</code> and
  <code>GameExperience.py</code>, which handled environment setup, state observation, and memory storage.
</p>

<h2>My Contribution</h2>
<p>
  I was given the base environment and helper classes, but I implemented the main training loop responsible for
  running multiple epochs, selecting actions, updating rewards, training the neural network, and tracking performance
  metrics like loss and win rate. Specifically, I added logic that determines when to explore versus exploit using the
  epsilon-greedy approach, stores experiences in memory, and trains the model iteratively:
</p>

<pre><code>
for epoch in range(n_epoch):
    loss = 0.0
    n_episodes = 0
    agent_cell = random.choice(qmaze.free_cells)
    qmaze.reset(agent_cell)
    env_state = qmaze.observe()
    while qmaze.game_status() == 'not_over':
        previous_env_state = env_state
        if np.random.uniform(0, 1) < epsilon:
            action = random.choice(qmaze.valid_actions())
        else:
            action = np.argmax(experience.predict(previous_env_state))
        env_state, reward, game_status = qmaze.act(action)
        episode = [previous_env_state, action, reward, env_state, game_status]
        experience.remember(episode)
        training_input, training_target = experience.get_data(data_size)
        model.fit(training_input, training_target, epochs=8, batch_size=16, verbose=0)
        loss = model.evaluate(training_input, training_target)
</code></pre>

<h2>Connection to Computer Science</h2>
<p>
  Through this project, I learned how reinforcement learning applies to real-world problem solving by combining
  exploration, exploitation, and model optimization. In the broader field of computer science, these principles are
  essential because they enable systems to adapt and improve over time without explicit programming.
</p>
<p>
  Computer scientists play a vital role in designing, analyzing, and implementing algorithms that make intelligent
  decisions — work that impacts industries like healthcare, automation, and cybersecurity. My approach to problem solving
  as a computer scientist now involves breaking down complex challenges into smaller, testable components, using logic,
  iteration, and data-driven methods.
</p>

<h2>Ethical Responsibilities</h2>
<p>
  Ethical responsibility is critical in AI development. As a computer scientist, I must ensure that my algorithms are
  transparent, fair, and secure. In this project, that means considering how reinforcement learning agents use data,
  respecting user privacy, and preventing biased or unintended outcomes. Building responsible AI not only protects users
  but also builds trust in technology.
</p>
