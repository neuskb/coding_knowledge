#include <iostream>
#include <set>
#include <vector>
using namespace std;


struct ListNode {
    int val;
    ListNode* next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode* next) : val(x), next(next) {}
};




int main()
{
    ListNode* head = new ListNode(-1);

    // 创建链表
    ListNode* tmp1 = head;
    vector<int> vec = {10, 9, 8, 7, 6};
    for (auto v : vec) {
        ListNode* node = new ListNode(v);
        tmp1->next = node;
        tmp1 = tmp1->next;
    }

    // 打印链表
    ListNode* tmpPrint = head;
    while (tmpPrint != nullptr) {
        cout << "create list tmp val:" << tmpPrint->val << endl;
        tmpPrint = tmpPrint->next;
    }

    // 在固定节点后插入一个节点
    int insertVal = -2;
    int insertBeforeVal = 8;
    ListNode* tmp3 = head;
    while (tmp3) {
        if (tmp3->val == 8) {
            ListNode* tmp3Next = tmp3->next;
            ListNode* newNode = new ListNode(-2);
            tmp3->next = newNode;
            newNode->next = tmp3Next;
            break;
        }
        tmp3 = tmp3->next;
    }

    // 打印链表
    tmpPrint = head;
    while (tmpPrint != nullptr) {
        cout << "insert list tmp val:" << tmpPrint->val << endl;
        tmpPrint = tmpPrint->next;
    }

    // 删除一个中间的固定节点
    int deleteVal = -2;
    ListNode* tmp5 = head;
    while (tmp5->next != nullptr && tmp5->next->next != nullptr) {
        if (tmp5->next->val == deleteVal) {
            tmp5->next = tmp5->next->next;
            break;
        }
        tmp5 = tmp5->next;
    }

    // 打印链表
    tmpPrint = head;
    while (tmpPrint != nullptr) {
        cout << "delete list tmp val:" << tmpPrint->val << endl;
        tmpPrint = tmpPrint->next;
    }

    // 将链表反转
    ListNode* pre = nullptr;
    ListNode* cur = head;
    while (cur) {
        ListNode* tmpNode = cur->next;
        cur->next = pre;
        pre = cur;
        cur = tmpNode;
    }

    // 打印链表
    head = pre;
    tmpPrint = head;
    while (tmpPrint != nullptr) {
        cout << "reverse list tmp val:" << tmpPrint->val << endl;
        tmpPrint = tmpPrint->next;
    }

    // 删除倒数第2个节点
    // 快慢指针方式
    ListNode* slow = head;
    ListNode* fast = head;
    int n = 2;
    // 快指针先走n步
    while (n) {
        fast = fast->next;
        n--;
    }

    // 快慢同时走
    while (nullptr != fast->next) {
        fast = fast->next;
        slow = slow->next;
    }

    slow->next = slow->next->next;

    // 打印链表
    tmpPrint = head;
    while (tmpPrint != nullptr) {
        cout << "delete1 list tmp val:" << tmpPrint->val << endl;
        tmpPrint = tmpPrint->next;
    }

    return 0;
}
