package coverage

import (
	"os"
	"reflect"
	"testing"
	"time"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW

func isMatrixShallowEqual(m1 Matrix, m2 Matrix) bool {
	if m1.rows == m2.rows && m1.cols == m2.cols && len(m1.data) == len(m2.data) { return true}
	return false
}

func isMatrixDeepEqual(m1 Matrix, m2 Matrix) bool {
	if !isMatrixShallowEqual(m1, m2) { return false }

	for i,v := range m1.data {
		if v != m2.data[i] { return false }
	}

	return true
}

func isSliceEqual(a, b [][]int) bool {
	if len(a) != len(b) {
			return false
	}
	for i, v := range a {
		if len(v) != len(b[i]) {
			return false
		}
		for j, d := range a[i] {
			if d != b[i][j] {
					return false
			}
		}
	}
	return true
}

func getTestMatrix() (string, *Matrix, [][]int, [][]int, *Matrix) {
	seedMatrix := "1 2 3\n4 5 6\n7 8 9"
	etalonMatrix := Matrix{
		rows: 3,
		cols: 3,
		data: []int{1, 2, 3, 4, 5, 6, 7, 8, 9},
	}
	rows := [][]int{
		{1, 2, 3},
		{4, 5, 6},
		{7, 8, 9},
	}
	cols := [][]int{
		{1, 4, 7},
		{2, 5, 8},
		{3, 6, 9},
	}
	changedMatrix := Matrix{
		rows: 3,
		cols: 3,
		data: []int{1, 2, 3, 4, 0, 6, 7, 8, 9},
	}
	
	return seedMatrix, &etalonMatrix, rows, cols, &changedMatrix
}

func getBedStructuredMatrix() string {
	return "1 2 3\n4 5 6 0\n7 8 9"
}

func getBedValueMatrix() string {
	return "1 2 3\n4 a 6\n7 8 9"
}

func TestNewMatrixOk(t *testing.T) {
	seedMatrix, etalonMatrix, _, _, _ := getTestMatrix()
	m, _ := New(seedMatrix)
	if !isMatrixDeepEqual(*m, *etalonMatrix) {
		t.Errorf("Matrix created not properly")
	}
}

func TestNewMatrix_ErrBedStructure(t *testing.T) {
	_, err := New(getBedStructuredMatrix())
	if err == nil {
		t.Errorf("expected to get an error")
	}

}
func TestNewMatrix_ErrBedValue(t *testing.T) {
	_, err := New(getBedValueMatrix())
	if err == nil {
		t.Errorf("expected to get an error")
	}
}

func TestRowsMethodOk(t *testing.T) {
	seed, _, rows, _, _ := getTestMatrix()
	m, _ := New(seed)
	resRows := m.Rows()

	if !isSliceEqual(resRows, rows) {
		t.Errorf("Rows slice not correct")
	}

}
func TestColsMethodOk(t *testing.T) {
	seed, _, _, cols, _ := getTestMatrix()
	m, _ := New(seed)
	resCols := m.Cols()

	if !isSliceEqual(resCols, cols) {
		t.Errorf("Cols slice not correct")
	}
}

func TestSetMethodOk(t *testing.T) {
	seed, _, _, _, _ := getTestMatrix()
	m, _ := New(seed)
	_ = m.Set(1, 1, 0)

	if !reflect.DeepEqual(m.data, []int{1, 2, 3, 4, 0, 6, 7, 8, 9}) {
		t.Errorf("Set not correct")
	}
}

func TestSetMethodErr(t *testing.T) {
	seed, _, _, _, _ := getTestMatrix()
	m, _ := New(seed)

	isTruthly := m.Set(-1, 1, 0 )
	if isTruthly {
		t.Errorf("For negative row index wants falsy result but got truthly")
	}

	isTruthly = m.Set(1, -1, 0 )
	if isTruthly {
		t.Errorf("For negative col index wants falsy result but got truthly")
	}

	isTruthly = m.Set(3, 1, 0 )
	if isTruthly {
		t.Errorf("For out of range row index wants falsy result but got truthly")
	}

	isTruthly = m.Set(1, 3, 0 )
	if isTruthly {
		t.Errorf("For out of range col index wants falsy result but got truthly")
	}
}

func getPeople() (*People, *People){
	ps0 := Person{
		firstName: "Igor",
		lastName: "Sechenov",
		birthDay: time.Date(1978, 8, 2, 0, 0, 0, 0, time.UTC),
	}

	ps1 := Person{
		firstName: "Igor",
		lastName: "Tkachuk",
		birthDay: time.Date(1978, 8, 2, 0, 0, 0, 0, time.UTC),
	
	}
	
	ps2 := Person{
		firstName: "Leonid",
		lastName: "Tkachuk",
		birthDay: time.Date(1978, 8, 2, 0, 0, 0, 0, time.UTC),
	}

	ps3 := Person{
		firstName: "Leonid",
		lastName: "Tkachuk",
		birthDay: time.Date(1979, 8, 2, 0, 0, 0, 0, time.UTC),
	}

	return &People{ps0, ps1, ps2, ps3}, &People{ps1, ps0, ps2, ps3} 
}

func TestPeopleLenOk(t *testing.T){
	p, _ := getPeople()
	l := p.Len()
	if l != 2 {
		t.Errorf("Wants 2 got %d", l)
	}

}
func TestPeopleSwapOk(t *testing.T){
	p, swapedP := getPeople()
	
	p.Swap(0, 1)

	if !reflect.DeepEqual(p, swapedP) {
		t.Errorf("Swap is not work properly")
	}
}

func TestPeopleLesOk(t *testing.T){
	p, _ := getPeople()

	isTruthly := p.Less(0, 1)
	if !isTruthly {
		t.Errorf("Less is not work properly")
	}

	isTruthly = p.Less(1, 2)
	if !isTruthly {
		t.Errorf("Less is not work properly")
	}

	isTruthly = p.Less(2, 3)
	if !isTruthly {
		t.Errorf("Less is not work properly")
	}
}