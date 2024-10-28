# 24-midterm


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
    	panel.setLayout(new GridLayout(4,4));
    	
    	// 버튼 위치
    	String[] buttons = {
    			"7", "8", "9", "/",
    			"4", "5", "6", "*",
    			"1", "2", "3", "-",
    			"0", "=", "+", "C"
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
