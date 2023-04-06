# Capture-the-Flag
## Synopsis
A 2 or 4 player game of luck and strategy. Last team standing wins!

## Motivation
I have always been a fan of strategy games both in real life and on the computer. Building this custom game has allowed me to do both

## How to Run
You will need the sourse code and a java SDK that runs version 1.8 or you will have to convert the project into a JavaFX project for latter versions of the SDK.

## Code Example
This is the movePiece() method, it handles all movement, captures, and any update to the main board. It has complex logic to sort the proper action when a piece is moved.

'''
public boolean movePiece(Piece selectedPiece, int startRow, int startColumn, int endRow, int endColumn,
                             int die1, int die2) {
        if ((startRow - endRow <= 1 && startRow - endRow >= -1) &&
                (startColumn - endColumn <= 1 && startColumn - endColumn >= -1) &&
                (startRow - endRow == 0 ^ startColumn - endColumn == 0)) {
            if (pieceLocation[endRow][endColumn] != null) {
                // if the piece moved to is a flag
                if (pieceLocation[endRow][endColumn].isFlag) {
                    String color = pieceLocation[endRow][endColumn].getFlagColor();
                    if (selectedPiece.getPawnColor().equals(color) && !(selectedPiece.isPawnWithFlag)) {
                        if (selectedPiece.getPawnColor().equals("Blue") && endRow != 0 && endColumn != 2
                                && pieceLocation[0][2] == null) {
                            pieceLocation[0][2] = new Piece("Blue");
                            remove(endRow, endColumn);
                            return true;
                        } else if (selectedPiece.getPawnColor().equals("Green") && endRow != 2 && endColumn != 4
                                && pieceLocation[2][4] == null) {
                            pieceLocation[2][4] = new Piece("Green");
                            remove(endRow, endColumn);
                            return true;
                        } else if (selectedPiece.getPawnColor().equals("Yellow") && endRow != 4 && endColumn != 2
                                && pieceLocation[4][2] == null) {
                            pieceLocation[4][2] = new Piece("Yellow");
                            remove(endRow, endColumn);
                        } else if (selectedPiece.getPawnColor().equals("Red") && endRow != 2 && endColumn != 0
                                && pieceLocation[2][0] == null) {
                            pieceLocation[2][0] = new Piece("Red");
                            remove(endRow, endColumn);
                        } else {
                            return false;
                        }
                    } else if (selectedPiece.isPawnWithFlag && selectedPiece.getPawnColor().equals(color)) {
                        checkAndRemoveFlag(selectedPiece, endRow, endColumn);
                        return true;
                    } else {
                        pieceLocation[endRow][endColumn] = selectedPiece;
                        selectedPiece.setPawnWithFlag(true);
                        selectedPiece.setFlagColor(color);
                        remove(startRow, startColumn);
                        return true;
                    }
                    // if the piece is a pawn
                } else if (capturePiece(die1, die2)) {
                    if (pieceLocation[endRow][endColumn].isPawnWithFlag) {
                        String color = pieceLocation[endRow][endColumn].getFlagColor();
                        pieceLocation[endRow][endColumn] = selectedPiece;
                        remove(startRow, startColumn);
                        switch (color) {
                            case "Blue" :
                                if (pieceLocation[0][2] != null) {
                                    pieceLocation[startRow][startColumn] = selectedPiece;
                                }
                                pieceLocation[0][2] = new Piece("Blue");
                                break;
                            case "Green" :
                                if (pieceLocation[2][4] != null) {
                                    pieceLocation[startRow][startColumn] = selectedPiece;
                                }
                                pieceLocation[2][4] = new Piece("Green");
                                break;
                            case "Yellow" :
                                if (pieceLocation[4][2] != null) {
                                    pieceLocation[startRow][startColumn] = selectedPiece;
                                }
                                pieceLocation[4][2] = new Piece("Yellow");
                                break;
                            case "Red" :
                                if (pieceLocation[2][0] != null) {
                                    pieceLocation[startRow][startColumn] = selectedPiece;
                                }
                                pieceLocation[2][0] = new Piece("Red");
                                break;
                        }
                    } else {
                        String color = pieceLocation[endRow][endColumn].getPawnColor();
                        if (selectedPiece.pawnColor.equals(color)) {
                            System.out.println("Invalid move");
                            return false;
                        } else {
                            pieceLocation[endRow][endColumn] = selectedPiece;
                            remove(startRow, startColumn);
                        }
                    }
                    return true;
                }
            } else {
                if (selectedPiece.isPawnWithFlag) {
                    checkAndRemoveFlag(selectedPiece, endRow, endColumn);
                }
                pieceLocation[endRow][endColumn] = selectedPiece;
                remove(startRow, startColumn);
            }
            return true;
        } else return false;
    }
'''

## Tests
I used JUnit 4 to test this program. If further tesing is desired use can use the pre-existing tests in the source code to further the testing process.

## Contributors
Chauncy Wilson - Myself
