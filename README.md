# personal_lizhonglo
#include <bits/stdc++.h>  
template<typename T>  
class myVector  
{  
public:  
    myVector():array(0),count(0),allocCount(0)  
    {  
    }  
    myVector(const T& t,unsigned int n):array(0),count(0),allocCount(0)  
    {  
        while(n--)  
        {  
            push_back(t);  
        }  
    }   
    myVector(const myVector<T>& other):array(0),count(0),allocCount(0)  
    {  
        *this = other;  
    }    
    myVector<T>& operator =(myVector<T>& other)  
    {  
        if(this == &other)  
            return *this;  
  
        clear();  
  
        count = other.size();  
        allocCount = other.allocSize();  
        array = new T[allocCount];  
        for(unsigned int i = 0 ;i<count;++i)  
        {  
            array[i] = other[i];  
        }  
  
        return *this;  
    }  

    ~myVector()  
    {  
        clear();  
    }  
  
    T& operator[](unsigned int pos)  
    {  
        assert(pos<count);  
        return array[pos];  
    }  
    unsigned int size()  
    {  
        return count;  
    }  
  
    unsigned int allocSize()  
    {  
        return allocCount;  
    }  
      
    bool empty()  
    {  
        return count == 0;  
    }  
  
    void clear()  
    {  
        deallocator(array);  
        array = 0;  
        count = 0;  
        allocCount = 0;  
    }     
    void push_back(const T& t)  
    {  
        insert_after(count-1,t);  
    }    
    void push_front(const T& t)  
    {  
        insert_before(0,t);  
    }   
    void insert_after(int pos,const T& t)  
    {  
        insert_before(pos+1,t);  
    }  
    void insert_before(int pos,const T& t)  
    {  
        if(count==allocCount)  
        {  
            T* oldArray = array;  
  
            allocCount += WALK_LENGTH;   
            array = allocator(allocCount);  
            for(unsigned int i = 0 ;i<count;++i)  
            {  
                array[i] = oldArray[i];  
            }  
            deallocator(oldArray);  
        }  
  
        for(int i = (int)count++;i>pos;--i)  
        {  
            array[i] = array[i-1];  
        }  
        array[pos] = t;  
    }  
    void erase(unsigned int pos)  
    {  
        if(pos<count)  
        {  
            --count;  
            for(unsigned int i = pos;i<count;++i)  
            {  
                array[i] = array[i+1];  
            }  
        }  
    }  
  
private:  
    T*  allocator(unsigned int size)  
    {  
        return new T[size];  
    }  
  
    void deallocator(T* arr)  
    {  
        if(arr)  
            delete[] arr;  
    }  
private:  
    T*              array;  
    unsigned int    count;  
    unsigned int    allocCount;  
};  
#endif  
[html] view plaincopy
void printfVector(myVector<int>& vector1)  
{  
    for(unsigned int i = 0 ; i < vector1.size();++i)  
    {  
        cout<<vector1[i]<<",";  
    }  
    cout<<"alloc size = "<<vector1.allocSize()<<",size = "<<vector1.size()<<endl;  
}  
  
void main()  
{  
    myVector<int> myVector1;  
    myVector<int> myVector2(0,10);  
    myVector2.push_front(1);  
    myVector2.erase(11);  
    printfVector(myVector2);  
    myVector1.push_back(2);  
    myVector1.push_front(1);  
    printfVector(myVector1);  
    myVector1.insert_after(1,3);  
    printfVector(myVector1);  
    myVector2 = myVector1;  
    myVector2.insert_before(0,0);  
    myVector2.insert_before(1,-1);  
    printfVector(myVector2);  
} ng
