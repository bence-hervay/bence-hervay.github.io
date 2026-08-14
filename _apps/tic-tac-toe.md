---
layout: page
title: Tic-tac-toe
permalink: /apps/tic-tac-toe/
description: A trivial local demo — no AI, no networking, just X and O on one screen.
img:
importance: 1
---

A minimal demo app: a clickable 3×3 grid, alternating X and O, that detects a win or
a draw. Fully static and client-side — no server, no network, no AI opponent, no
external dependencies. It exists to prove the `/apps/` collection pattern works, not
to be a polished game.

<div id="ttt-app" class="ttt-app">
  <p class="ttt-status" id="ttt-status">X's turn</p>
  <div class="ttt-board" id="ttt-board"></div>
  <button type="button" class="ttt-reset" id="ttt-reset">Reset</button>
</div>

<style>
  .ttt-app {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 1.5rem 0;
  }
  .ttt-status {
    font-size: 1.1rem;
    margin-bottom: 0.75rem;
  }
  .ttt-board {
    display: grid;
    grid-template-columns: repeat(3, 72px);
    grid-template-rows: repeat(3, 72px);
    gap: 4px;
  }
  .ttt-cell {
    width: 72px;
    height: 72px;
    font-size: 2rem;
    line-height: 1;
    font-weight: 600;
    background: rgba(128, 128, 128, 0.12);
    border: 1px solid rgba(128, 128, 128, 0.35);
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0;
  }
  .ttt-cell:disabled {
    cursor: default;
  }
  .ttt-cell.ttt-win {
    background: rgba(80, 200, 120, 0.35);
  }
  .ttt-reset {
    margin-top: 1rem;
    padding: 0.4rem 1rem;
    cursor: pointer;
  }
</style>

<script>
(function () {
  var board = document.getElementById('ttt-board');
  var status = document.getElementById('ttt-status');
  var resetButton = document.getElementById('ttt-reset');

  var LINES = [
    [0, 1, 2], [3, 4, 5], [6, 7, 8], // rows
    [0, 3, 6], [1, 4, 7], [2, 5, 8], // columns
    [0, 4, 8], [2, 4, 6]             // diagonals
  ];

  var cells = [];
  var marks = [];
  var currentPlayer = 'X';
  var gameOver = false;

  function checkResult() {
    for (var i = 0; i < LINES.length; i++) {
      var line = LINES[i];
      var a = marks[line[0]], b = marks[line[1]], c = marks[line[2]];
      if (a && a === b && b === c) {
        return { winner: a, line: line };
      }
    }
    if (marks.every(function (m) { return m !== null; })) {
      return { winner: null, line: null, draw: true };
    }
    return null;
  }

  function render() {
    status.textContent = currentPlayer + "'s turn";
  }

  function endGame(result) {
    gameOver = true;
    cells.forEach(function (cell) { cell.disabled = true; });
    if (result.draw) {
      status.textContent = "Draw!";
    } else {
      status.textContent = result.winner + " wins!";
      result.line.forEach(function (i) { cells[i].classList.add('ttt-win'); });
    }
  }

  function handleClick(index) {
    if (gameOver || marks[index] !== null) return;
    marks[index] = currentPlayer;
    cells[index].textContent = currentPlayer;
    cells[index].disabled = true;

    var result = checkResult();
    if (result) {
      endGame(result);
      return;
    }

    currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
    render();
  }

  function reset() {
    marks = [null, null, null, null, null, null, null, null, null];
    currentPlayer = 'X';
    gameOver = false;
    cells.forEach(function (cell) {
      cell.textContent = '';
      cell.disabled = false;
      cell.classList.remove('ttt-win');
    });
    render();
  }

  function build() {
    for (var i = 0; i < 9; i++) {
      var cell = document.createElement('button');
      cell.type = 'button';
      cell.className = 'ttt-cell';
      cell.setAttribute('aria-label', 'cell ' + (i + 1));
      (function (idx) {
        cell.addEventListener('click', function () { handleClick(idx); });
      })(i);
      board.appendChild(cell);
      cells.push(cell);
      marks.push(null);
    }
    resetButton.addEventListener('click', reset);
    render();
  }

  build();
})();
</script>
