# 24-midterm
/*
 * @2024-10-28 생성
 * @계산기 프레임 제작
 * @배열 변경 : 4x4에서 5x4로 변경 빈칸과 . 버튼 추가로 인해 빈칸 무시하는 코드 생성.
 * @배경색을 검정으로 변경하고 텍스트필드의 글씨를 흰색으로 변경., 메인패널 생성
 * @버튼의 모양을 동그랗게 변경. ->취소
 * @버튼의 색깔변경.
 * @색깔 변경 코드를 짧게 변경 (첫번째줄 밝은회색/ 오른쪽 세로줄 주황/ 나머지 어두운회색)
 * @AC 옆 빈버튼 +/-와 %로 변경 기능은 구현하지 못했음.
 * 텍스트필드 사이즈를 키움
 * 텍스트필드에 나오는 폰트 사이즈를키움
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

    	// 전체 배경을 담을 메인 패널 생성
        JPanel mainPanel = new JPanel();
        mainPanel.setLayout(new BorderLayout());
        mainPanel.setBackground(Color.BLACK);  // 메인 패널 배경색 검정
	
    	display = new JTextField(); //텍스트필드 칸에 결과, 숫자 보여주기
    	display.setEditable(false); //직접 입력 못하게 설정
    	display.setHorizontalAlignment(JTextField.RIGHT); //오른쪽 정렬 
    	display.setBackground(Color.BLACK);               // 텍스트 필드 배경색 검정
        display.setForeground(Color.WHITE);               // 텍스트 필드 텍스트색 흰색
	display.setPreferredSize(new Dimension(400, 100)); // 텍스트 필드 크기 조정
    	
    	//패널설정(그리드 레이아웃 사용)
    	JPanel panel = new JPanel();
    	panel.setLayout(new GridLayout(5,4)); // 4*4에서 5*4로 변경
     	panel.setBackground(Color.BLACK);  // 버튼 패널 배경색 검정
    	
    	// 버튼 위치
    	String[] buttons = {
    		"AC", "+/-", "%", "/",
                "7", "8", "9", "*",
                "4", "5", "6", "-",
                "1", "2", "3", "+",
                "0", "", ".", "="
    	};
    	
    	for (String text : buttons) {
    		JButton button = new JButton(text); //버튼 생성
    		button.addActionListener(this); //클릭

       // ➜ **버튼 모양을 동그랗게 설정**
            button.setFocusPainted(false);       // 버튼에 포커스 표시 제거
            button.setBorder(BorderFactory.createEmptyBorder()); // 기본 테두리 제거
            button.setContentAreaFilled(false);   // 버튼의 배경색 채우기 제거
	    button.setOpaque(true);                // 버튼의 불투명성 설정

            // ➜ **동그란 버튼 만들기: 버튼의 모양을 원으로 설정**
            button.setPreferredSize(new Dimension(60, 60)); // 버튼 크기 설정
            button.setBackground(Color.DARK_GRAY); // 버튼 배경색 설정
            button.setForeground(Color.WHITE);      // 버튼 텍스트 색상 설정

     	// ➜ **버튼 색상 설정**
            if (text.equals("AC") || text.equals("") || text.equals(" ")) {
                button.setBackground(Color.LIGHT_GRAY); // AC와 빈 버튼은 밝은 회색
            } else if (text.equals("/") || text.equals("*") || text.equals("-") || text.equals("+") || text.equals("=")) {
                button.setBackground(Color.ORANGE); // 연산자는 주황색
            } else {
                button.setBackground(Color.DARK_GRAY); // 나머지 숫자는 어두운 회색
            }

            button.setForeground(Color.WHITE);      // 버튼 텍스트 색상 설정
            
            // ➜ **버튼에 마우스 오버 효과 추가**
            button.addMouseListener(new java.awt.event.MouseAdapter() {
                @Override
                public void mouseEntered(java.awt.event.MouseEvent evt) {
                    button.setBackground(Color.GRAY); // 마우스 오버 시 색상 변경
                }

                @Override
                public void mouseExited(java.awt.event.MouseEvent evt) {
                 // 원래 색상으로 복원
                 if (text.equals("AC") || text.equals("+/-") || text.equals("%")) {
                     button.setBackground(Color.LIGHT_GRAY); // 밝은 회색으로 복원
                 } else if (text.equals("/") || text.equals("*") || text.equals("-") || text.equals("+") || text.equals("=")) {
                     button.setBackground(Color.ORANGE); // 주황색으로 복원
                 } else {
                     button.setBackground(Color.DARK_GRAY); // 어두운 회색으로 복원
                 }
             }
         });

         button.setPreferredSize(new Dimension(60, 60)); // 버튼 크기 설정
         panel.add(button);                    // 패널에 버튼 추가
     }
    	
    	//레이아웃 설정: 텍스트필드 위,버튼 아래 -> mainPanel로 변경
    	mainPanel.add(display, BorderLayout.NORTH);
    	mainPanel.add(panel, BorderLayout.CENTER);
    	
    	// ➜ **메인 패널을 JFrame에 추가**
        setContentPane(mainPanel);
    	
    	setTitle("계산기"); //제목
    	setSize(300,400); //크기
    	setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); //창 닫기
    	setVisible(true); //창 보이게 설정
    }

/*
     * @GPT 도움받아 계산기능 추가.
     * @ 빈칸 무시 기능 생성.
     * @ UI 꾸미기 도움받음.
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
     
