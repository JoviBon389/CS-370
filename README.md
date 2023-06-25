# CS-370

1.) Briefly explain the work that you did on this project: What code were you given? What code did you create yourself?

We were tasked with creating the code for the Q-Training Alogrithm. We were given a GameExperience.py and a TreasureMaze.py to help with the functionality, as well as the majority of the treasure hunt game starter code.
The specific code we had to create ourselves is as follows:

 for epoch in range(n_epoch):

        loss = 0
        n_episodes = 0
        Agent_cell = random.choice(qmaze.free_cells)
        qmaze.reset(Agent_cell)
        envstate = qmaze.observe()
        game_over = False
        
       # In [17] #     
        while not game_over:
            previous_envstate = envstate
            q = model.predict(previous_envstate)
            action = np.argmax(q[0])
            envstate, reward, game_status = qmaze.act(action)
            if game_status == 'lose':
                win_history.append(0)
                game_over = True
            elif game_status == 'win':
                win_history.append(1)
                game_over = True
            else:
                game_over = False
            
            # Yeah I had no idea how to do this bit, had to have outside help honestly
            episode = [previous_envstate, action, reward, envstate, game_status]
            experience.remember(episode)
            n_episodes += 1
            inputs, targets = experience.get_data()
            history = model.fit(inputs, targets, epochs=8, batch_size=24, verbose=0)
            loss = model.evaluate(inputs, targets)      
           
        # win rate is determined by dividing the sum of total history of win/lose game by the length of episodes
        win_rate = sum(win_history) / len(win_history)

2.) Connect your learning from throughout this course to the larger field of computer science:
What do computer scientists do and why does it matter?

Computer scientists design and develop hardware and software that is used as solutions for business, industry, scientific, and social contexts.

How do I approach a problem as a computer scientist?

The best way to approach a problem is to identify what it is for starters. Then, break it down into smaller parts, solve the individual split components on their own, and then try to integrate the solutions together so it all functions correctly. 

What are my ethical responsibilities to the end user and the organization?

My ethical responsibilities are to provide a service or product that the end user finds agreeable, all while not compromising my standing with the orgnization that funds me. All of this which is balanced out by my own personal views, ethics, and morals.
