# -
第六組五子棋
#ifndef ChessBoard_h
#define ChessBoard_h
const int n = 15;
int chessBoardInfor[n][n];
class ChessBoard {

public:
	ChessBoard();
	void initWindow();
	void drawChessBoard(int x, int y);
};
#endif // !Chessboard_h

