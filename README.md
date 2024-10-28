# 24-midterm
/*
 * @2024-10-28 생성
 * @계산기 프레임 제작
 * @배열 변경 : 4x4에서 5x4로 변경 빈칸과 . 버튼 추가로 인해 빈칸 무시하는 코드 생성.
 */

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

//JFrame을받아 GUI창 생성
public class MidtermCalculator extends JFrame implements ActionListener {
	
	private JTextField display;//텍스트필드 칸 생성
    private String operator; //연산자
    private double num1, num2; //1번숫자 2번숫자
    
    //GUI 구성요소설청, 창설정.
    public MidtermCalculator() {
    	display = new JTextField(); //텍스트필드 칸에 결과, 숫자 보여주기
    	display.setEditable(false); //직접 입력 못하게 설정
    	display.setHorizontalAlignment(JTextField.RIGHT); //오른쪽 정렬 
    	
    	//패널설정(그리드 레이아웃 사용)
    	JPanel panel = new JPanel();
    	panel.setLayout(new GridLayout(5,4)); // 4*4에서 5*4로 변경
    	
    	// 버튼 위치
    	String[] buttons = {
    		"AC", "", "", "/",
                "7", "8", "9", "*",
                "4", "5", "6", "-",
                "1", "2", "3", "+",
                "0", "", ".", "="
    	};
    	
    	for (String text : buttons) {
    		JButton button = new JButton(text); //버튼 생성
    		button.addActionListener(this); //클릭
    		panel.add(button); //패널에 버튼 추가
    	}
    	
    	//레이아웃 설정: 텍스트필드 위,버튼 아래
    	add(display, BorderLayout.NORTH);
    	add(panel, BorderLayout.CENTER);
    	
    	setTitle("계산기"); //제목
    	setSize(300,400); //크기
    	setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); //창 닫기
    	setVisible(true); //창 보이게 설정
    }

/*
     * @GPT 도움받아 계산기능 추가.
     * @ 빈칸 무시 기능 생성.
     */

     
//버튼 클릭했을때 동작 정의
    @Override
    public void actionPerformed(ActionEvent e) {
    	String command = e.getActionCommand();

	if (command.equals("")) return; //빈칸 무시기능 생성
     	
    	//숫자 버튼 클릭
    	if("0123456789".contains(command)) {
    		display.setText(display.getText() + command);
    	}
    	//c 버튼 화면 초기화 기능
    	else if (command.equals("C")) {
    		display.setText("");
    		num1 = num2 = 0;
    		operator = "";
    	}
    	// = 버튼 계산
    	else if (command.equals("=")) {
    		num2 = Double.parseDouble(display.getText());
    		switch (operator) {
    		case "+":display.setText(String.valueOf(num1 + num2)); break;
    		case "-":display.setText(String.valueOf(num1 - num2)); break;
    		case "*":display.setText(String.valueOf(num1 * num2)); break;
    		case "/":display.setText(String.valueOf(num1 / num2)); break;
    		}
    	}
    	// 연산자 버튼 
    	else {
    		operator = command; //현재 연산자 저장
    		num1 = Double.parseDouble(display.getText()); //첫번째 숫자 저장
    		display.setText(""); //화면 초기화 하고 두번째 숫자 입력
    	}
    }
	public static void main(String[] args) {
		new MidtermCalculator();
	}

}
     
