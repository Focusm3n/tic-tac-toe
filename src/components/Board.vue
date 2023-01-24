<template>
    <div class="board">
        <label>Сейчас ходит {{board.whoWalks}}</label>
            <table class="table">
                <tr class="column" v-for="column in board.fields">
                    <td class="line" @click="put(field)" v-for="field in column"><div v-if="field.value">{{ field.value }}</div></td>
                </tr>
            </table>
        <button @click="generateBoard()">Сгенерировать доску</button>
    </div>
</template>

<script>
export default {
    name: 'Board',
    data() {
        return {
            board: {
                title: 'Игра в крестики нолики',
                whoWalks: 'X',
                fields: [],
            },
        }
    },
    props: {
        size: Number,
    },
    mounted() {
        this.generateBoard();
    },
    methods: {
        generateBoard() {
            this.board.fields = [];
            for (let i = 0; i < this.size; i++) {
                let tmp = [];
                for (let j = 0; j < this.size; j++) {
                    tmp.push({ column: i, line: j, value: 0 })
                }
                this.board.fields.push(tmp)
            }
        },
        put(field) {
            if (field.value === 0) {
                if (this.board.whoWalks === 'X') {
                    this.board.fields[field.column][field.line].value = 'X'
                    this.board.whoWalks = 'O'
                } else {
                    this.board.fields[field.column][field.line].value = 'O'
                    this.board.whoWalks = 'X'
                }
            }
            this.checkWinVertical(field)
            this.checkWinHorizontal(field)
            this.checkWinDiagonal(field)

        },
        checkWinVertical(field) {
            let value = this.board.fields[field.column][field.line].value;
            let x = field.line;
            let y = field.column - 1;
            let win = 1;

            while(y >= 0 && y < this.size) {
                if (this.board.fields[y][x].value === value) {
                    win++;
                    y--;
                    if (win === 5) {
                        this.win(value);
                    }
                    continue;
                }
                break;
            }
            y = field.column + 1;
            while(y >= 0 && y < this.size) {
                if (this.board.fields[y][x].value === value) {
                    win++;
                    y++;
                    if (win === 5) {
                        this.win(value);
                    }
                    continue;
                }
                break;
            }

        },
        checkWinHorizontal(field) {
            let value = this.board.fields[field.column][field.line].value;
            let x = field.line - 1;
            let y = field.column;
            let win = 1;

            while(x >= 0 && x < this.size) {
                if (this.board.fields[y][x].value === value) {
                    win++;
                    x--;
                    if (win === 5) {
                        this.win(value);
                    }
                    continue;
                }
                break;
            }
            x = field.line + 1;
            while(x >= 0 && x < this.size) {
                if (this.board.fields[y][x].value === value) {
                    win++;
                    x++;
                    if (win === 5) {
                        this.win(value);
                    }
                    continue;
                }
                break;
            }
        },
        checkWinDiagonal(field) {
            let value = this.board.fields[field.column][field.line].value;
            let x = field.line - 1;
            let y = field.column - 1;
            let win = 1;


            while(x >= 0 && x < this.size && y >= 0 && y < this.size) {
                if (this.board.fields[y][x].value === value) {
                    win++;
                    x--;
                    y--;
                    if (win === 5) {
                        this.win(value);
                    }
                    continue;
                }
                break;
            }
            x = field.line + 1;
            y = field.column + 1;
            while(x >= 0 && x < this.size && y >= 0 && y < this.size) {
                if (this.board.fields[y][x].value === value) {
                    win++;
                    x++;
                    y++;
                    if (win === 5) {
                        this.win(value);
                    }
                    continue;
                }
                break;
            }

            win = 1;
            x = field.line + 1;
            y = field.column - 1
            while(x >= 0 && x < this.size && y >= 0 && y < this.size) {
                if (this.board.fields[y][x].value === value) {
                    win++;
                    x++;
                    y--;
                    if (win === 5) {
                        this.win(value);
                    }
                    continue;
                }
                break;
            }
            x = field.line - 1;
            y = field.column + 1;
            while(x >= 0 && x < this.size && y >= 0 && y < this.size) {
                if (this.board.fields[y][x].value === value) {
                    win++;
                    x--;
                    y++;
                    if (win === 5) {
                        this.win(value);
                    }
                    continue;
                }
                break;
            }

        },
        win(value) {
            let message = 'Победил ' + value + '\nПоздравляю!!!';
            alert(message);
        }
    },
}
</script>

<style scoped>
.board {
    margin: 30px;
}

h3 {
    margin: 40px 0 0;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}

.line {
    width: 23px;
    height: 23px;
}

.line{
    border: 1px solid darkblue;
    padding: 8px;
    margin-left: 30px;
}

.table {
    border-collapse: collapse;
}
</style>
