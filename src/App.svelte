<script>
  let activeTab = 'pomodoro';
  let minutes = 25;
  let seconds = 0;
  let isRunning = false;
  let timerInterval;

  function selectTab(tab) {
    activeTab = tab;
    if (tab === 'pomodoro') {
      minutes = 25;
    } else if (tab === 'short') {
      minutes = 5;
    } else if (tab === 'long') {
      minutes = 15;
    }
    seconds = 0;
    isRunning = false;
    clearInterval(timerInterval);  
  }

  function toggleTimer() {
    if (isRunning) {
      clearInterval(timerInterval);
      isRunning = false;
    } else {
      isRunning = true;
      timerInterval = setInterval(() => {
        if (seconds === 0) {
          if (minutes === 0) {
            clearInterval(timerInterval);
            isRunning = false;
           
          } else {
            minutes--;
            seconds = 59;
          }
        } else {
          seconds--;
        }
      }, 1000);
    }
  }

  function resetTimer() {
  isRunning = false;
  clearInterval(timerInterval);

  if (activeTab === 'pomodoro') {
    minutes = 25;
  } else if (activeTab === 'short') {
    minutes = 5;
  } else if (activeTab === 'long') {
    minutes = 15;
  }
  seconds = 0;
}

</script>

<div class="timer-container">
  <div class="tabs">
    <button class="pomodoro" class:selected={activeTab === 'pomodoro'} on:click={() => selectTab('pomodoro')}>Pomodoro</button>
    <button class="short" class:selected={activeTab === 'short'} on:click={() => selectTab('short')}>Short Break</button>
    <button class="long" class:selected={activeTab === 'long'} on:click={() => selectTab('long')}>Long Break</button>
  </div>

  <h2>{minutes}:{seconds < 10 ? `0${seconds}` : seconds}</h2>
</div>

<button on:click={toggleTimer}>
  {isRunning ? 'Pause' : 'Start'}
</button>

<button on:click={resetTimer}>
  Reset
</button>

<style>
  
  .timer-container {
    background: #f9f9f9;
    padding: 2rem;
    border-radius: 12px;
    max-width: 450px;
    margin: 3rem auto;
    text-align: center;
    box-shadow: 0 4px 12px rgba(0,0,0,0.05);
    
}

  .tabs {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin-bottom: 2rem;
  }

  .tabs button {
    padding: 0.5rem 1.5rem;
    border: none;
    background: #ddd;
    color: black;
    border-radius: 8px;
    font-size: 1rem;
    cursor: pointer;
    transition: background 0.2s ease;
  }

  .tabs button.selected {
    color: black;
  }

  .tabs button.selected.pomodoro {
    background: #d9534f; 
  }

  .tabs button.selected.short {
    background: #5cb85c; 
  }

  .tabs button.selected.long {
    background: #339af0;
  }

  .tabs button:focus {
    outline: none;
}

  h2 {
    color: black;
    font-size: 4rem;
    margin: 1rem 0;
  }

  button {
    padding: 0.7rem 2rem;
    border: none;
    background: #333;
    color: white;
    border-radius: 8px;
    font-size: 1rem;
    cursor: pointer;
    margin-top: 1.5rem;
    transition: background 0.2s ease;
}

button:hover {
    background: #555;
}

button:focus {
    outline: none;
}
</style>
