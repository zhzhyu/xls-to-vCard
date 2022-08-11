# coding=utf-8
from csv import excel
from nturl2path import url2pathname
import os
import time
from openpyxl import load_workbook
from ui import Ui_MainWindow
from PySide6.QtWidgets import QApplication, QMainWindow,QFileDialog,QMessageBox,QProgressBar
from PySide6.QtGui import QIcon

def utf(file):
    with open(file,'r',encoding='gbk') as f:
        content =f.read()
    with open(file,'w',encoding='utf8') as f:
        f.write(content)

def etov(uurl):
    wb = load_workbook(uurl)
    vcf = open('Vcard.vcf',mode='w')
    sheet=wb['Sheet1']
    a0=1
    a1=2
    b=2
    T=True
    while(T):
        name=str(sheet.cell(b,a0).value)
        phone=str(sheet.cell(b,a1).value)
        vcf.write('BEGIN:VCARD\n')
        vcf.write('VERSION:3.0\n')
        vcf.writelines(['N;CHARSET=utf-8:;'+name+';;;\n'])
        vcf.writelines(['FN;CHARSET=utf-8: '+name+'\n'])
        vcf.writelines(['TEL;CELL:'+phone+'\n'])
        vcf.write('END:VCARD\n')
        b=b+1
        T=sheet.cell(b,a0).value!=None

    vcf.close()
    wb.close()
    utf('.\\Vcard.vcf')
class MainWindow(QMainWindow):
    def __init__(self):
        super(MainWindow, self).__init__()
        self.ui = Ui_MainWindow()  # UI类的实例化()
        self.ui.setupUi(self)
        self.setWindowTitle("Excel转Vcard")
        self.setWindowIcon(QIcon("touxiang.ico"))
        self.bind()
    def bind(self):
        self.ui.excel.clicked.connect(self.eclick)
        self.ui.start.clicked.connect(self.bg)
    def eclick(self):
        self.uurl,_ = QFileDialog.getOpenFileName(self.ui.excel,"选择文件")
        self.ui.url.setText(self.uurl)
    def bg(self):
        etov(self.uurl)
        QMessageBox.information(self.ui.url,'操作成功','转换成功，浏览同目录下的vcf文件')


if __name__ == '__main__':
    app = QApplication([])  # 启动一个应用
    window = MainWindow()  # 实例化主窗口
    window.show()  # 展示主窗口
    app.exec()  # 避免程序执行到这一行后直接退出
